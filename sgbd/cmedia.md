# cmedia.prg

- Jobs: [68](#jobs)
- Tables: [86](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Combox_Media |
| ORIGIN | BMW EI44 Hr.Mallinson |
| REVISION | 2.018 |
| AUTHOR | HBAS EDB1 Aufrecht, HaysAG EI44 Hr.Bubb |
| COMMENT | COMBOXMAIN [11] |
| PACKAGE | 1.17 |
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
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Gibt an ob SG Most Ring wecken darf
- [STATUS_AVERAGE_MESSAGE_RECEPTION_RATE](#job-status-average-message-reception-rate) - Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein
- [STATUS_FOT_TEMPERATUR](#job-status-fot-temperatur) - Gibt an ob SG Most Ring wecken darf
- [STATUS_ROUTING_ENGINE](#job-status-routing-engine) - Inhalt der Routing Engine
- [STATUS_VERSION_MOST_CONTROLLER](#job-status-version-most-controller) - Return Version of MOST Controller
- [STATUS_VERSORGUNGSSPANNUNG](#job-status-versorgungsspannung) - Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.
- [STATUS_WAKEUP_STATUS](#job-status-wakeup-status) - Gibt an, ob das SG den MOST-Ring geweckt hat oder geweckt wurde.
- [STEUERN_ABILITY_TO_WAKE](#job-steuern-ability-to-wake) - Gibt an, ob das SG den MOST-Ring wecken darf.
- [STATUS_SENSOR_TEMP](#job-status-sensor-temp) - Returns the temperature of the desired sensor (no matter if the temperature is currently being simulated or not).
- [STEUERN_SENSOR_TEMP](#job-steuern-sensor-temp) - Simulates the temperature of a definite sensor.
- [STEUERN_WATCHDOG_TRIGGER_STOP](#job-steuern-watchdog-trigger-stop) - Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
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
- [STATUS_SWUP_INSTALLED](#job-status-swup-installed) - UDS:     $22   ReadDataByIdentifier $4013 Status_Swup_Installed
- [LESEN_DAS](#job-lesen-das) - UDS:     $31   RoutineControl $03   StatusRoutine $F010 LESEN_DAS
- [LESEN_CONFIG_INIT_VALUES](#job-lesen-config-init-values) - UDS:     $31   RoutineControl $03   StatusRoutine $F011 LESEN_CONFIG_INIT_VALUES
- [LESEN_DASVP](#job-lesen-dasvp) - UDS:     $31   RoutineControl $03   StatusRoutine $F012 LESEN_DASVP
- [LESEN_CONTROL_LIST_MAINBOARD](#job-lesen-control-list-mainboard) - UDS:     $31   RoutineControl $03   StatusRoutine $F014 LESEN_CONTROL_LIST_MAINBOARD
- [LESEN_OTA](#job-lesen-ota) - UDS:     $31   RoutineControl $03   StatusRoutine $F005 LESEN_OTA
- [LESEN_DPAS](#job-lesen-dpas) - UDS:     $31   RoutineControl $03   StatusRoutine $F013 LESEN_DPAS
- [SCHREIBEN_OTA](#job-schreiben-ota) - UDS:     $31   RoutineControl $01   StatusRoutine $F005 SCHREIBEN_OTA
- [SCHREIBEN_BMW_ZERTIFIKATE](#job-schreiben-bmw-zertifikate) - UDS:     $31   RoutineControl $01   StatusRoutine $F00C SCHREIBEN_BMW_ZERTIFIKATE
- [SCHREIBEN_BROWSER_ZERTIFIKATE](#job-schreiben-browser-zertifikate) - UDS:     $31   RoutineControl $01   StatusRoutine $F00D SCHREIBEN_BROWSER_ZERTIFIKATE
- [WATCHDOG_TRIGGER_STOP](#job-watchdog-trigger-stop) - UDS:     $31   RoutineControl $01   StartRoutine $0209 WATCHDOG_TRIGGER_STOP
- [STATUS_BT_READ_PHONE_ID](#job-status-bt-read-phone-id) - Returns information about the phone selected as argument
- [STATUS_USB_STACK_INFO_FOR_DEVICE](#job-status-usb-stack-info-for-device) - Reads out logistical information about the four last connected USB devices four last connected IPOD Players, four last connected MTP Players and four last unrecognized USB devices
- [STATUS_USB_TEST_TEL](#job-status-usb-test-tel) - KWP2000: $31   StartRoutineByLocalIdentifier $03   Layer03 $A06A Status USB Test
- [STEUERN_USB_TEST_TEL](#job-steuern-usb-test-tel) - Stores VendorID and ProductID for diagnosis of USB mass storage recognition for USB Interface (KDZ = Kundenzugang in der Mittelkonsole) or and Telephone Snap In Adapter (SIA)
- [STATUS_POWERMANAGEMENT_SH4](#job-status-powermanagement-sh4) - Auslesen der gespeicherten internen Powermanagement Transitionen 

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
| STAT_ABILITY_TO_WAKE_TEXT | string | 0 = off, 1 = on,  2= critical ("critical" ist in Most Specs definiert wird aber praktisch nicht benutzt) |
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

<a id="job-status-sensor-temp"></a>
### STATUS_SENSOR_TEMP

Returns the temperature of the desired sensor (no matter if the temperature is currently being simulated or not).

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SENSOR | unsigned char | Sensor for which the temperature must be returned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATURE_WERT | char | Temperature of the selected sensor |
| STAT_DURATION_WERT | unsigned char | Remaining duration for the simulated temperature |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-sensor-temp"></a>
### STEUERN_SENSOR_TEMP

Simulates the temperature of a definite sensor.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SENSOR | unsigned char | Sensor for which the temperature must be simulated |
| ARG_TEMPERATURE | char | Temperature that must be simulated |
| ARG_DURATION | unsigned char | Duration of the temperature simulation |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-watchdog-trigger-stop"></a>
### STEUERN_WATCHDOG_TRIGGER_STOP

Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TIME_WATCHDOG | unsigned int | Beschreibung: z.B. ARG_TIME_WATCHDOG = 4 bedeutet Abschalten des Watchdog-Triggers nach 4 Sekunden. nur positiven Zahlen und die 0. Skalierung: 1 entspricht 1 Sekunde |

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

<a id="job-status-swup-installed"></a>
### STATUS_SWUP_INSTALLED

UDS:     $22   ReadDataByIdentifier $4013 Status_Swup_Installed

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_ANZAHL_SWUP | int | Anzahl der SWUP |
| STAT_SWUP_INSTALLED | string | Sind SWUP Pakete installiert |
| STAT_FREI_FLASHSPEICHER | unsigned long | Freier Flashspeicher |
| STAT_FREI_FLASHSPEICHER_EINH | string | Einhiet für Freier Flashspeicher |
| STAT_PROG_DATUM | string | Programmierdatum (DD.MM.YY) |
| STAT_PROG_KM | long | KM-Stand bei Programmierung (10 KM bis 655350 KM) |
| STAT_PROZESSKLASSE_WERT | int | dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_EINH | string | Einheit der dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT | string | Text-Angabe der Prozessklasse |
| STAT_SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION | string | Angabe der Version der Prozessklasse |
| STAT_ACTIVATION_STATUS | char | 0x00: inaktiv, 0x01: aktiv |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-lesen-das"></a>
### LESEN_DAS

UDS:     $31   RoutineControl $03   StatusRoutine $F010 LESEN_DAS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SMNC | string | Mobile Network Code von der SIM Karte, z.B: T-Online hat den Code 001 |
| ARG_SMCC | string | Mobile Country Code von der SIM Karte, z.B: Deutschland hat den Code 262 |
| ARG_NMNC | string | Mobile Network Code vom Netz, z.B: T-Online hat den Code 001 |
| ARG_NMCC | string | Mobile Country Code vom Netz, z.B: Deutschland hat den Code 262 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_DAS | binary | DAS daten |

<a id="job-lesen-config-init-values"></a>
### LESEN_CONFIG_INIT_VALUES

UDS:     $31   RoutineControl $03   StatusRoutine $F011 LESEN_CONFIG_INIT_VALUES

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_CONFIG_INIT_VALUES | binary | Init config Values |

<a id="job-lesen-dasvp"></a>
### LESEN_DASVP

UDS:     $31   RoutineControl $03   StatusRoutine $F012 LESEN_DASVP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_DASVP | binary | DASVP daten |

<a id="job-lesen-control-list-mainboard"></a>
### LESEN_CONTROL_LIST_MAINBOARD

UDS:     $31   RoutineControl $03   StatusRoutine $F014 LESEN_CONTROL_LIST_MAINBOARD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_CONTROL_LIST_MAINBOARD | binary | LESEN_CONTROL_LIST_MAINBOARD daten |

<a id="job-lesen-ota"></a>
### LESEN_OTA

UDS:     $31   RoutineControl $03   StatusRoutine $F005 LESEN_OTA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_OTA | binary | LESEN_OTA daten |

<a id="job-lesen-dpas"></a>
### LESEN_DPAS

UDS:     $31   RoutineControl $03   StatusRoutine $F013 LESEN_DPAS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_DPAS | string | LESEN_DPAS daten |

<a id="job-schreiben-ota"></a>
### SCHREIBEN_OTA

UDS:     $31   RoutineControl $01   StatusRoutine $F005 SCHREIBEN_OTA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PFAD | string | Pfad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-schreiben-bmw-zertifikate"></a>
### SCHREIBEN_BMW_ZERTIFIKATE

UDS:     $31   RoutineControl $01   StatusRoutine $F00C SCHREIBEN_BMW_ZERTIFIKATE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PFAD | string | Pfad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-schreiben-browser-zertifikate"></a>
### SCHREIBEN_BROWSER_ZERTIFIKATE

UDS:     $31   RoutineControl $01   StatusRoutine $F00D SCHREIBEN_BROWSER_ZERTIFIKATE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PFAD | string | Pfad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-watchdog-trigger-stop"></a>
### WATCHDOG_TRIGGER_STOP

UDS:     $31   RoutineControl $01   StartRoutine $0209 WATCHDOG_TRIGGER_STOP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TIME_WATCHDOG | unsigned int | time to make reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt-read-phone-id"></a>
### STATUS_BT_READ_PHONE_ID

Returns information about the phone selected as argument

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_EINTRAG_NR | unsigned char | Phone from which the information must be read out (possible values: 1, 2, 3 and 4) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_P_KM_READING_AT_LAST_RECONNECT | unsigned long | Mileage at the last reconnect of the phone selected as argument |
| STAT_P_NO_OF_RECONNECTS | unsigned int | Number of reconnects of the phone selected as argument |
| STAT_P_PHONE_MODEL_TRUNC_RAWDATA | string | Phone model as raw data |
| STAT_P_PHONE_SOFTWARE_TRUNC_RAWDATA | string | Phone software as raw data |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-usb-stack-info-for-device"></a>
### STATUS_USB_STACK_INFO_FOR_DEVICE

Reads out logistical information about the four last connected USB devices four last connected IPOD Players, four last connected MTP Players and four last unrecognized USB devices

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TYPE | unsigned char | UMS-type of requested Info 0x01 USB Stick 0x02 IPOD 0x03 MTP Player 0x04 UNKNOWN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_1_VENDORID_WERT | string | Vendor ID |
| STAT_1_PRODUCTID_WERT | string | Product ID |
| STAT_1_CLASSID_WERT | string | Class ID |
| STAT_1_SUBCLASSID_WERT | string | Subclass ID |
| STAT_1_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_1_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_1_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_1_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_1_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_1_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_1_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_1_USED_PORT | unsigned char | Port Info |
| STAT_2_VENDORID_WERT | string | Vendor ID |
| STAT_2_PRODUCTID_WERT | string | Product ID |
| STAT_2_CLASSID_WERT | string | Vendor ID |
| STAT_2_SUBCLASSID_WERT | string | Product ID |
| STAT_2_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_2_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_2_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_2_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_2_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_2_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_2_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_2_USED_PORT | unsigned char | Port Info |
| STAT_3_VENDORID_WERT | string | Vendor ID |
| STAT_3_PRODUCTID_WERT | string | Product ID |
| STAT_3_CLASSID_WERT | string | Vendor ID |
| STAT_3_SUBCLASSID_WERT | string | Product ID |
| STAT_3_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_3_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_3_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_3_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_3_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_3_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_3_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_3_USED_PORT | unsigned char | Port Info |
| STAT_4_VENDORID_WERT | string | Vendor ID |
| STAT_4_PRODUCTID_WERT | string | Product ID |
| STAT_4_CLASSID_WERT | string | Vendor ID |
| STAT_4_SUBCLASSID_WERT | string | Product ID |
| STAT_4_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_4_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_4_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_4_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_4_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_4_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_4_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_4_USED_PORT | unsigned char | Port Info |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-usb-test-tel"></a>
### STATUS_USB_TEST_TEL

KWP2000: $31   StartRoutineByLocalIdentifier $03   Layer03 $A06A Status USB Test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_USB_TEST_TEL_KDZ | unsigned char | Ergebnis des USB Schnittstelle Tests 0x00 Kein Gerät angeschlossen 0x01 Gerät angeschlossen, Erkennung läuft 0x02 Gerät erkannt aber falsche ID 0x03 Gerät angeschlossen und richtige ID 0xFE Gerät angeschlossen aber kein Massenspeicher 0xFF Nicht definiert |
| STAT_VENDORID_INT_TEL_KDZ_WERT | string | Hier wird die vorgegebene VendorID von STEUERN_USB_TEST_TEL für das Gerät von der USB Schnittstelle ausgegeben Hexwerte als string |
| STAT_PRODUCTID_INT_TEL_KDZ_WERT | string | Hier wird die vorgegebene ProductID von STEUERN_USB_TEST_TEL für das Gerät von der USB Schnittstelle ausgegeben Hexwerte als string |
| STAT_VENDORID_REC_TEL_KDZ_WERT | string | Hier wird die erkannte VendorID des Gerätes von der USB Schnittstelle ausgegeben Hexwerte als string |
| STAT_PRODUCTID_REC_TEL_KDZ_WERT | string | Hier wird die erkannte ProductID des Gerätes von der USB Schnittstelle ausgegeben Hexwerte als string |
| STAT_VENDORSTRING_KDZ_REC_WERT | string | Hier wird der erkannte VendorString des Gerätes von der USB Schnittstelle ausgegeben |
| STAT_USB_TEST_TEL_SIA | unsigned int | Ergebnis des Snap In Adpater Tests 0x00 Kein Gerät angeschlossen 0x01 Gerät angeschlossen, Erkennung läuft 0x02 Gerät erkannt aber falsche ID 0x03 Gerät angeschlossen und richtige ID 0xFE Gerät angeschlossen aber kein Massenspeicher 0xFF Nicht definiert |
| STAT_VENDORID_INT_TEL_SIA_WERT | string | Hier wird die vorgegebene VendorID von STEUERN_USB_TEST_TEL für das Telefon vom Snap In Adapter ausgegeben Hexwerte als string |
| STAT_PRODUCTID_INT_TEL_SIA_WERT | string | Hier wird die vorgegebene ProductID von STEUERN_USB_TEST_TEL für das Telefon vom Snap In Adapter ausgegeben Hexwerte als string |
| STAT_VENDORID_REC_TEL_SIA_WERT | string | Hier wird die erkannte VendorID des Gerätes vom Snap In Adapter ausgegeben Hexwerte als string |
| STAT_PRODUCTID_REC_TEL_SIA_WERT | string | Hier wird die erkannte ProductID des Gerätes vom Snap In Adapter ausgegeben Hexwerte als string |
| STAT_VENDORSTRING_SIA_REC_WERT | string | Hier wird der erkannte VendorString für das Gerätes vom Snap In Adapter ausgegeben |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-usb-test-tel"></a>
### STEUERN_USB_TEST_TEL

Stores VendorID and ProductID for diagnosis of USB mass storage recognition for USB Interface (KDZ = Kundenzugang in der Mittelkonsole) or and Telephone Snap In Adapter (SIA)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VENDORID_KDZ | string | referenz VendorID Kundenzugang |
| ARG_PRODUCTID_KDZ | string | referenz ProduktID Kundenzugang |
| ARG_VENDORID_SIA | string | referenz VendorID SNAPIn |
| ARG_PRODUCTID_SIA | string | referenz ProduktID SNAPIn |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-powermanagement-sh4"></a>
### STATUS_POWERMANAGEMENT_SH4

Auslesen der gespeicherten internen Powermanagement Transitionen 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DATASET | unsigned char | Dataset number requested Index starts with 0x01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_TEXT | string | values from table TPowerState |
| STAT_EVENT_TEXT | string | values from table TPowerEvent |
| STAT_TIMESTAMP | string | Timestamp as hex string |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (121 × 2)
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
- [TFBLOCKIDTEXTE](#table-tfblockidtexte) (37 × 2)
- [TMOSTLIGHT](#table-tmostlight) (2 × 2)
- [TWAKEUPSTATUS](#table-twakeupstatus) (3 × 3)
- [CBSKENNUNG](#table-cbskennung) (11 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (42 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (10 × 9)
- [IORTTEXTE](#table-iorttexte) (62 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (12 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (23 × 16)
- [TAB_TYPEUSBDEVICE](#table-tab-typeusbdevice) (5 × 2)
- [TUSBCONNECTIONSTATE](#table-tusbconnectionstate) (3 × 2)
- [TUSBINTERFACE](#table-tusbinterface) (3 × 2)
- [TUSBTESTSTATUS](#table-tusbteststatus) (6 × 2)
- [RES_0XD00B](#table-res-0xd00b) (4 × 10)
- [RES_0XD01A](#table-res-0xd01a) (1 × 10)
- [ARG_0XD01A](#table-arg-0xd01a) (1 × 12)
- [RES_0XD01B](#table-res-0xd01b) (1 × 10)
- [ARG_0XD01B](#table-arg-0xd01b) (1 × 12)
- [RES_0XD01C](#table-res-0xd01c) (1 × 10)
- [ARG_0XD01C](#table-arg-0xd01c) (1 × 12)
- [RES_0XD01D](#table-res-0xd01d) (4 × 10)
- [RES_0XD01E](#table-res-0xd01e) (64 × 10)
- [TSOFTWAREUPDATETYP](#table-tsoftwareupdatetyp) (6 × 2)
- [TSOFTWAREUPDATEERRORCODE](#table-tsoftwareupdateerrorcode) (44 × 2)
- [RES_0XD035](#table-res-0xd035) (2 × 10)
- [ARG_0XD035](#table-arg-0xd035) (1 × 12)
- [TLASTCONNECTIONTEL](#table-tlastconnectiontel) (2 × 2)
- [TSIMSTATUS](#table-tsimstatus) (8 × 2)
- [RES_0XD047](#table-res-0xd047) (65 × 10)
- [TREMOTESERVICES](#table-tremoteservices) (4 × 2)
- [TDOORSSTATUS](#table-tdoorsstatus) (3 × 2)
- [RES_0XD057](#table-res-0xd057) (2 × 10)
- [THUBCONNECTIONSTATE](#table-thubconnectionstate) (4 × 2)
- [TAB_TDAACTIVATIONSTATE](#table-tab-tdaactivationstate) (5 × 2)
- [RES_0XD099](#table-res-0xd099) (2 × 10)
- [RES_0XA019](#table-res-0xa019) (35 × 13)
- [ARG_0XA019](#table-arg-0xa019) (1 × 14)
- [TAUXVERBINDUNG](#table-tauxverbindung) (6 × 2)
- [TVERBINDUNGFEHLERART](#table-tverbindungfehlerart) (4 × 2)
- [RES_0XA022](#table-res-0xa022) (2 × 13)
- [ARG_0XA022](#table-arg-0xa022) (1 × 14)
- [TSELBSTTESTROUTINE](#table-tselbsttestroutine) (2 × 2)
- [RES_0XA046](#table-res-0xa046) (3 × 13)
- [TPROVISIONINGSTATUSTEL](#table-tprovisioningstatustel) (6 × 2)
- [RES_0XA048](#table-res-0xa048) (1 × 13)
- [ARG_0XA048](#table-arg-0xa048) (1 × 14)
- [TBLUETOOTHSTATUS](#table-tbluetoothstatus) (3 × 2)
- [RES_0XA049](#table-res-0xa049) (1 × 13)
- [ARG_0XA049](#table-arg-0xa049) (1 × 14)
- [TBLUETOOTHDISCOVERYMODESTATUS](#table-tbluetoothdiscoverymodestatus) (3 × 2)
- [RES_0XA04C](#table-res-0xa04c) (6 × 13)
- [ARG_0XA04C](#table-arg-0xa04c) (1 × 14)
- [TBLUETOOTHRESET](#table-tbluetoothreset) (5 × 2)
- [TBLUETOOTHRESETBASICSTATE](#table-tbluetoothresetbasicstate) (9 × 2)
- [RES_0XA04F](#table-res-0xa04f) (51 × 13)
- [ARG_0XA04F](#table-arg-0xa04f) (1 × 14)
- [TANTENNECMEDIA](#table-tantennecmedia) (3 × 2)
- [TANTENNEFEHLERART](#table-tantennefehlerart) (5 × 2)
- [RES_0XA050](#table-res-0xa050) (2 × 13)
- [ARG_0XA050](#table-arg-0xa050) (1 × 14)
- [TVERBAUCMEDIA](#table-tverbaucmedia) (7 × 2)
- [TTESTSTATUS](#table-tteststatus) (6 × 2)
- [RES_0XA05A](#table-res-0xa05a) (1 × 13)
- [RES_0XA079](#table-res-0xa079) (1 × 13)
- [TRESETSTATUS](#table-tresetstatus) (6 × 2)
- [RES_0XF015](#table-res-0xf015) (1 × 13)
- [TA4ASTRINGSTATUS](#table-ta4astringstatus) (2 × 2)
- [TSOFTWAREUPDATEPROZESSKLASSE](#table-tsoftwareupdateprozessklasse) (22 × 2)
- [TPOWERSTATE](#table-tpowerstate) (7 × 2)
- [TPOWEREVENT](#table-tpowerevent) (23 × 2)

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

Dimensions: 121 rows × 2 columns

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

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 42 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x023600 | Energiesparmode aktiv | 0 |
| 0x02FF36 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 |
| 0xB7F180 | Software Reset | 0 |
| 0xB7F181 | Mikrofon 1: Kurzschluss nach Plus | 0 |
| 0xB7F182 | Mikrofon 2: Kurzschluss nach Plus | 0 |
| 0xB7F183 | Bluetooth-Antenne: Kurzschluss nach Plus | 0 |
| 0xB7F184 | AUX-Verbindung rechts: Kurzschluss nach Plus | 0 |
| 0xB7F185 | AUX-Verbindung links: Kurzschluss nach Plus | 0 |
| 0xB7F186 | AUX-Verbindung links: Kurzschluss nach Masse | 0 |
| 0xB7F187 | AUX-Verbindung rechts: Kurzschluss nach Masse | 0 |
| 0xB7F188 | Mikrofon 1: Kurzschluss nach Masse | 0 |
| 0xB7F189 | Mikrofon 2: Kurzschluss nach Masse | 0 |
| 0xB7F18A | USB-Anschluss: Abschaltung wegen Überlastung | 1 |
| 0xB7F18B | Snap-in-Adapter (USB-Anschluss): Abschaltung wegen Überlastung | 1 |
| 0xB7F191 | Mikrofon 2: Unterbrechung | 0 |
| 0xB7F192 | Mikrofon 1: Unterbrechung | 0 |
| 0xB7F193 | Bluetooth-Antenne: Unterbrechung | 0 |
| 0xB7F1A0 | interner Steuergerätefehler (ERROR RAM) | 0 |
| 0xB7F1A1 | interner Steuergerätefehler (Flash Speicher) | 0 |
| 0xB7F1A2 | interner Steuergerätefehler (INIC PCode) | 0 |
| 0xB7F1A3 | interner Steuergerätefehler (DRM Chip) | 0 |
| 0xB7F1A4 | interner Steuergerätefehler (USB Chip) | 0 |
| 0xB7F1A5 | interner Steuergerätefehler (Ethernet Chip) | 0 |
| 0xB7F1A6 | interner Steuergerätefehler (FPGA) | 0 |
| 0xB7F1A7 | interner Steuergerätefehler (Bluecore Chip) | 0 |
| 0xB7F1B0 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0xB7F1B1 | Codierung: Fehler bei Codierung aufgetreten | 0 |
| 0xB7F1B2 | Codierung: Signatur für Daten ungültig | 0 |
| 0xB7F1B3 | Codierung: Codierung passt nicht zum Fahrzeug | 0 |
| 0xB7F1B4 | Codierung: Unplausible Daten während Transaktion | 0 |
| 0xB7F1B5 | Überspannung | 1 |
| 0xB7F1B6 | ungültige Bluetooth-Adresse | 0 |
| 0xB7F2E0 | KISU Speicher oder Dateisystem defekt | 0 |
| 0xB7F2E1 | KISU Inkonsistenter Systemzustand | 0 |
| 0xB7F2E3 | Hardware Reset | 0 |
| 0xB7F2E4 | KISU Systemmonitor: Deinstallation nach Dauerreset | 0 |
| 0xB7F2EF | KISU Unspezifizierter Systemdefekt oder inkonsistenter Systemzustand | 0 |
| 0xD6843F | MOST: Empfänger hat Nachricht nicht abgenommen | 1 |
| 0xD68442 | Abschaltung Übertemperatur | 1 |
| 0xD68445 | MOST: Reset | 0 |
| 0xD68BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur fuer Testzwecke | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 3 |
| F_HLZ_VIEW | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1707 | Diagnoseadresse eines verdächtigen Steuergeräts | Hex | - | unsigned char | - | - | - | - |
| 0x1708 | Aktueller Klemmenstatus im System mit EB-Zustand | Hex | - | unsigned char | - | - | - | - |
| 0x1709 | MOST Nachrichten Header | text | - | 6 | - | - | - | - |
| 0x170A | Temperatur, gemessen in unmittelbarer Nähe der FOT | Grad C | - | signed char | - | - | - | - |
| 0x170B | Node Position, aktuelle physikalische Position eines SG im MOST Ring relativ zum TimingMaster | Hex | - | unsigned char | - | - | - | - |
| 0x170C | Versorgungsspannung am Eingang des SG | mV | high | unsigned int | - | - | - | - |
| 0x1721 | Reset Grund | Hex | - | unsigned char | - | - | - | - |
| 0xF000 | Interner Reset-Grund | Hex | high | signed long | - | - | - | - |
| 0xF001 | FZGS_Fehlercode | Hex | - | unsigned char | - | - | - | - |
| 0xF003 | Spannung am Eingang des Mikrophons | mV | high | unsigned int | - | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 62 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xB7F190 | Fehler beim CSM (Client Security Model) aufgetreten | 1 |
| 0xB7F194 | INIC Memory Error | 1 |
| 0xB7F195 | Passwort Fehler: Passwort wurde drei mal falsch eingegeben | 1 |
| 0xB7F196 | HBHK Daten wurden wieder hergestellt | 1 |
| 0xB7F197 | Filesystem Fehler: Filesystem wurde wieder hergestellt | 1 |
| 0xB7F1B7 | BT Linkloss | 1 |
| 0xB7F1B8 | DisconnectByDeviceDriver | 1 |
| 0xB7F1B9 | InvalidBTAddressOfConnectedDevice | 1 |
| 0xB7F1BA | IdleCatching | 1 |
| 0xB7F1BB | Mikrofon 1: Kurzschluss nach Plus | 0 |
| 0xB7F1BC | Mikrofon 1: Kurzschluss nach Masse | 0 |
| 0xB7F1BD | Mikrofon 1: Unterbrechung | 0 |
| 0xB7F1BE | Mikrofon 2: Kurzschluss nach Plus | 0 |
| 0xB7F1BF | Mikrofon 2: Kurzschluss nach Masse | 0 |
| 0xB7F1C0 | Mikrofon 2: Unterbrechung | 0 |
| 0xB7F201 | KISU Fahrzeug steht nicht | 0 |
| 0xB7F202 | KISU Update Abbruch | 0 |
| 0xB7F203 | KISU MOST Kommunikationsfehler | 0 |
| 0xB7F204 | KISU SWUP-Quelle antwortet nicht | 0 |
| 0xB7F205 | KISU Gerät ausgelastet | 0 |
| 0xB7F20F | KISU Unspezifizierter Umweltfehler | 0 |
| 0xB7F210 | KISU Update bereits installiert | 0 |
| 0xB7F211 | KISU Update veraltet | 0 |
| 0xB7F21F | KISU Unspezifizierter Versionsfehler | 0 |
| 0xB7F220 | KISU I-Stufe des Fahrzeugs veraltet | 0 |
| 0xB7F221 | KISU SWUP-Zielgerät nicht verfügbar | 0 |
| 0xB7F222 | KISU Abhängigkeiten nicht erfüllt | 0 |
| 0xB7F223 | KISU Betroffene SWE nicht gefunden | 0 |
| 0xB7F224 | KISU Pre-Installation Skriptfehler | 0 |
| 0xB7F225 | KISU Post-Installation Skriptfehler | 0 |
| 0xB7F226 | KISU Fahrgestellnummer stimmt nicht überein | 0 |
| 0xB7F22F | KISU Unspezifizierter Fehler: Updatekompatibiliät | 0 |
| 0xB7F230 | KISU SWUP-Weiterleitung nicht unterstützt | 0 |
| 0xB7F231 | KISU Nicht genügend RAM | 0 |
| 0xB7F232 | KISU Nicht genügend Flashspeicher | 0 |
| 0xB7F233 | KISU System überlastet | 0 |
| 0xB7F234 | KISU SWUP-Paket zu groß | 0 |
| 0xB7F235 | KISU SWUP Paket oder SWIP Datei Weiterleitung fehlgeschlagen | 0 |
| 0xB7F236 | KISU Angefordertes SWUP Paket nicht verfügbar | 0 |
| 0xB7F23F | KISU Unspezifizierter Ressourcenfehler | 0 |
| 0xB7F240 | KISU SWIP-Signaturverifikation fehlgeschlagen | 0 |
| 0xB7F241 | KISU SWIP-XML-Datei korrupt | 0 |
| 0xB7F242 | KISU SWUP Hash Validierung fehlgeschlagen | 0 |
| 0xB7F243 | KISU SWUP korrupt oder unerwartetes Format | 0 |
| 0xB7F244 | KISU SWUP-Signaturverifikation fehlgeschlagen | 0 |
| 0xB7F24F | KISU Unspezifizierter Fehler: Integrität oder Authentisierung | 0 |
| 0xB7F250 | KISU SWUP-Download abgebrochen | 0 |
| 0xB7F251 | KISU Keine Verbindung für Over-The-Air Update | 0 |
| 0xB7F25F | KISU Unspezifizierter Over-The-Air-Fehler | 0 |
| 0xB7F260 | KISU Deinstallationsinformationen nicht verfügbar | 0 |
| 0xB7F261 | KISU Pre-Deinstallation Skriptfehler | 0 |
| 0xB7F262 | KISU Post-Deinstallation Skriptfehler | 0 |
| 0xB7F26F | KISU Unspezifizierter Deinstallationsfehler | 0 |
| 0xB7F270 | KISU Keine Update-Datei verfügbar | 0 |
| 0xB7F271 | KISU Update läuft | 0 |
| 0xB7F272 | KISU USB-Gerät nicht angeschlossen | 0 |
| 0xB7F27F | KISU Unspezifizierter Betriebssystemfehler | 0 |
| 0xB7F280 | KISU Angefordertes SWUP Paket via Teleservice Update nicht verfügbar | 0 |
| 0xB7F281 | KISU SWUP Paket oder SWIP Datei zu groß für die Übertragung via Teleservice Update | 0 |
| 0xB7F28F | KISU Unspezifizierter Teleservice Fehler | 0 |
| 0xB7F2FF | KISU unspezifizierter Fehler | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1707 | Diagnoseadresse eines verdächtigen Steuergeräts | Hex | - | unsigned char | - | - | - | - |
| 0x1708 | Aktueller Klemmenstatus im System mit EB-Zustand | Hex | - | unsigned char | - | - | - | - |
| 0x1709 | MOST Nachrichten Header | text | - | 6 | - | - | - | - |
| 0x170A | Temperatur, gemessen in unmittelbarer Nähe der FOT | Grad C | - | signed char | - | - | - | - |
| 0x170B | Node Position, aktuelle physikalische Position eines SG im MOST Ring relativ zum TimingMaster | Hex | - | unsigned char | - | - | - | - |
| 0x170C | Versorgungsspannung am Eingang des SG | mV | high | unsigned int | - | - | - | - |
| 0x1721 | Reset Grund | Hex | - | unsigned char | - | - | - | - |
| 0xF000 | Interner Reset-Grund | Hex | high | signed long | - | - | - | - |
| 0xF001 | FZGS_Fehlercode | Hex | - | unsigned char | - | - | - | - |
| 0xF002 | Speicheradresse | Hex | high | signed long | - | - | - | - |
| 0xF003 | Spannung am Eingang des Mikrophons | mV | high | unsigned int | - | - | - | - |
| 0x4100 | BT Adresse | text | - | 6 | - | - | - | - |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 23 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BT | 0xA048 | - | aktiviert/dekativiert Bluetooth | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA048 | RES_0xA048 |
| BT_ERKENNUNGSMODUS | 0xA049 | - | Steuerung Bluetooth Erkennungsmodus | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA049 | RES_0xA049 |
| BT_GERAETEADRESSE | 0xD01A | - | Steuert die Bluetooth Geräteadresse | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD01A | RES_0xD01A |
| BT_GERAETENAME | 0xD01C | - | Schreibt/Liest den Bluetooth Gerätenamen | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD01C | RES_0xD01C |
| BT_PASSKEY | 0xD01B | - | Schreibt/Liest den Bluetooth Passkey | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD01B | RES_0xD01B |
| DELETE_A4A_STRING | 0xF015 | - | This job shall delete the Protocol String com.bmw.a4a This job shall return if the Protocol String com.bmw.a4a is present | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xF015 |
| LAST_CONNECTION_TEL | 0xD035 | - | Auslesen des SIM Status und IP Adresse der letzte Verbindung Argument beschreibt welches Gerät für das die letze Verbindung abgefragt wird | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xD035 | RES_0xD035 |
| PROVISIONING_TEL | 0xA046 | - | Status des Provisionierungsprozess | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA046 |
| RESET_TO_DEFAULTCONFIG | 0xA079 | - | Setzt die standard Telematik Konfigurationswerte zurück und löscht die OTA (Over The Air) Daten | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA079 |
| SELBSTTEST | 0xA022 | - | Selbsttests des Steuergerätes Sie sollen einen evtl. notwendigen Tausch von Software/Hardware erkennen. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA022 | RES_0xA022 |
| STATUS_BT_GEKOPPELTE_GERAETE_LESEN | 0xD01D | - | Liest die Geräte-Adresse der letzten vier gekoppelten Bluetooth Geräte | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD01D |
| STATUS_REMOTE_SERVICES_LOG | 0xD047 | - | not defined in diagnosis database | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD047 |
| STATUS_SWUP_INSTALLATION_HISTORY | 0xD01E | - | Auslesen der letzten Software Update Installationen. Für jeden Eintrag werden Zeit, Operationtype, SWIP ID, ECU SW VID und Operationcode gespeichert. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD01E |
| STATUS_TDA_AKTIVIERUNG | 0xD091 | STAT_DIENSTE_AKTIVIERUNG | Status Aktivierung BMW Dienste durch Anwender | 0-n | - | - | unsigned char | TAB_TDAActivationState | - | - | - | - | 22 | - | - |
| STATUS_USB_HUB_TEST | 0xD057 | - | Status USB HUB eingebaut | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD057 |
| STATUS_USB_STECKZYKLEN | 0xD099 | - | Auslesen der USB Steckzyklen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD099 |
| STATUS_VERSION_ID_LESEN | 0xD00B | - | Auslesen Fahrgestellnummer, Hardware Lieferung ID, Software Lieferung ID und Steuergeräte Softwareupdate Version ID. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD00B |
| STEUERN_BT_DELETE_ALL_PHONE_ID | 0xA04B | - | Löschen angekoppelter Bluetooth Devices | - | - | - | - | - | - | - | - | - | 31 | - | - |
| STEUERN_RESET_TO_BASIC_STATE | 0xA04C | - | Löschen persönlicher Informationen Auswahl gemäß Tabelle TCMedia_Reset ACHTUNG: Manche Daten werden erst mit dem nächsten Reset vollständig entfernt! Erst dann ist die HMI wieder konsistent! | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA04C | RES_0xA04C |
| SWUP_REMOVE_CUSTOMER_UPDATES | 0xA05A | - | Entfernen aller Benutzer Updates. Fehlerfreien 1. Stand Wiederherstellen | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA05A |
| TEST_ANTENNE_TEL | 0xA04F | - | Startet und bewertet die Prüfung für eine oder mehrere Antennen. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA04F | RES_0xA04F |
| TEST_AUXVERBINDUNG | 0xA019 | - | Testet, ob die Aux-Anschlüsse verbaut sind. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA019 | RES_0xA019 |
| TEST_VERBAU_TEL | 0xA050 | - | Test Antenne Telefon | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA050 | RES_0xA050 |

<a id="table-tab-typeusbdevice"></a>
### TAB_TYPEUSBDEVICE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | USB Stick |
| 0x02 | IPOD |
| 0x03 | MTP Player |
| 0x04 | UNKNOWN |
| 0xFF | nicht definiert |

<a id="table-tusbconnectionstate"></a>
### TUSBCONNECTIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht angeschlossen |
| 0x01 | angeschlossen |
| 0xFF | nicht definiert |

<a id="table-tusbinterface"></a>
### TUSBINTERFACE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | USB Interface |
| 0x01 | Snap In Adapter |
| 0xFF | nicht definiert |

<a id="table-tusbteststatus"></a>
### TUSBTESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Gerät angeschlossen |
| 0x01 | Gerät angeschlossen, Erkennung läuft |
| 0x02 | Gerät erkannt aber falsche ID |
| 0x03 | Gerät angeschlossen und richtige ID |
| 0xFE | Gerät angeschlossen aber kein Massenspeicher |
| 0xFF | Nicht definiert |

<a id="table-res-0xd00b"></a>
### RES_0XD00B

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VIN_WERT | - | - | string | - | - | - | - | - | VIN: Fahrgestellnummer |
| STAT_HARDWARE_LIEFERUNG_WERT | - | - | string | - | - | - | - | - | HLI: Hardware Lieferung ID |
| STAT_SOFTWARE_LIEFERUNG_WERT | - | - | string | - | - | - | - | - | SOLI: Software Lieferung ID |
| STAT_ECU_SW_VID_WERT | - | - | string | - | - | - | - | - | ECU_SW_VID siehe Software Version ID Version 2.2. Beispiel: SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 |

<a id="table-res-0xd01a"></a>
### RES_0XD01A

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_GERAETEADRESSE_WERT | - | - | data[6] | - | - | - | - | - | Liefert die Adresse des Bluetooth Gerätes |

<a id="table-arg-0xd01a"></a>
### ARG_0XD01A

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT_GERAETEADRESSE | - | - | data[6] | - | - | - | - | - | - | - | Schreibt die Adresse des Bluetooth Gerätes |

<a id="table-res-0xd01b"></a>
### RES_0XD01B

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_PASSKEY_WERT | - | - | string | - | - | - | - | - | BT Passkey lesen |

<a id="table-arg-0xd01b"></a>
### ARG_0XD01B

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT_PASSKEY_WERT | - | - | string | - | - | - | - | - | - | - | BT Passkey schreiben |

<a id="table-res-0xd01c"></a>
### RES_0XD01C

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_GERAETENAME_WERT | - | - | string | - | - | - | - | - | Liest den Bluetooth Gerätenamen |

<a id="table-arg-0xd01c"></a>
### ARG_0XD01C

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT_GERAETENAME | - | - | string | - | - | - | - | - | - | - | Schreibt den Bluetooth Gerätenamen |

<a id="table-res-0xd01d"></a>
### RES_0XD01D

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_ADR_DEV_1_WERT | - | - | data[6] | - | - | - | - | - | Geräteadresse von Gerät 1 |
| STAT_BT_ADR_DEV_2_WERT | - | - | data[6] | - | - | - | - | - | Geräteadresse von Gerät 2 |
| STAT_BT_ADR_DEV_3_WERT | - | - | data[6] | - | - | - | - | - | Geräteadresse von Gerät 3 |
| STAT_BT_ADR_DEV_4_WERT | - | - | data[6] | - | - | - | - | - | Geräteadresse von Gerät 4 |

<a id="table-res-0xd01e"></a>
### RES_0XD01E

Dimensions: 64 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HISTORY_1_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 1. Historyeintrag |
| STAT_HISTORY_1_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 1. Historyeintrag |
| STAT_HISTORY_1_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 1. Historyeintrag |
| STAT_HISTORY_1_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 1. Historyeintrag |
| STAT_HISTORY_1_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 1. Historyeintrag |
| STAT_HISTORY_1_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 1. Historyeintrag |
| STAT_HISTORY_1_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 1. Historyeintrag |
| STAT_HISTORY_1_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 1. Historyeintrag |
| STAT_HISTORY_2_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 2. Historyeintrag |
| STAT_HISTORY_2_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 2. Historyeintrag |
| STAT_HISTORY_2_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 2. Historyeintrag |
| STAT_HISTORY_2_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 2. Historyeintrag |
| STAT_HISTORY_2_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 2. Historyeintrag |
| STAT_HISTORY_2_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 2. Historyeintrag |
| STAT_HISTORY_2_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 2. Historyeintrag |
| STAT_HISTORY_2_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 2. Historyeintrag |
| STAT_HISTORY_3_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 3. Historyeintrag |
| STAT_HISTORY_3_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 3. Historyeintrag |
| STAT_HISTORY_3_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 3. Historyeintrag |
| STAT_HISTORY_3_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 3. Historyeintrag |
| STAT_HISTORY_3_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 3. Historyeintrag |
| STAT_HISTORY_3_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 3. Historyeintrag |
| STAT_HISTORY_3_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 3. Historyeintrag |
| STAT_HISTORY_3_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 3. Historyeintrag |
| STAT_HISTORY_4_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 4. Historyeintrag |
| STAT_HISTORY_4_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 4. Historyeintrag |
| STAT_HISTORY_4_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 4. Historyeintrag |
| STAT_HISTORY_4_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 4. Historyeintrag |
| STAT_HISTORY_4_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 4. Historyeintrag |
| STAT_HISTORY_4_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 4. Historyeintrag |
| STAT_HISTORY_4_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 4. Historyeintrag |
| STAT_HISTORY_4_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 4. Historyeintrag |
| STAT_HISTORY_5_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 5. Historyeintrag |
| STAT_HISTORY_5_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 5. Historyeintrag |
| STAT_HISTORY_5_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 5. Historyeintrag |
| STAT_HISTORY_5_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 5. Historyeintrag |
| STAT_HISTORY_5_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 5. Historyeintrag |
| STAT_HISTORY_5_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 5. Historyeintrag |
| STAT_HISTORY_5_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 5. Historyeintrag |
| STAT_HISTORY_5_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 5. Historyeintrag |
| STAT_HISTORY_6_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 6. Historyeintrag |
| STAT_HISTORY_6_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 6. Historyeintrag |
| STAT_HISTORY_6_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 6. Historyeintrag |
| STAT_HISTORY_6_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 6. Historyeintrag |
| STAT_HISTORY_6_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 6. Historyeintrag |
| STAT_HISTORY_6_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 6. Historyeintrag |
| STAT_HISTORY_6_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 6. Historyeintrag |
| STAT_HISTORY_6_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 6. Historyeintrag |
| STAT_HISTORY_7_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 7. Historyeintrag |
| STAT_HISTORY_7_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 7. Historyeintrag |
| STAT_HISTORY_7_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 7. Historyeintrag |
| STAT_HISTORY_7_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 7. Historyeintrag |
| STAT_HISTORY_7_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 7. Historyeintrag |
| STAT_HISTORY_7_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 7. Historyeintrag |
| STAT_HISTORY_7_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 7. Historyeintrag |
| STAT_HISTORY_7_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 7. Historyeintrag |
| STAT_HISTORY_8_KILOMETER_WERT | km | - | unsigned long | - | - | - | - | - | Kilometerstand bei der Operation 8. Historyeintrag |
| STAT_HISTORY_8_ZEIT_WERT | - | - | string | - | - | - | - | - | Datum und Zeit YYYY-MM-DD_HH:MM 8. Historyeintrag |
| STAT_HISTORY_8_TYP | 0-n | - | unsigned char | - | TSoftwareUpdateTyp | - | - | - | Typ der Operation 8. Historyeintrag |
| STAT_HISTORY_8_SGBM_IDENTIFIER_WERT | - | - | string | - | - | - | - | - | Angabe SGBM-ID der Prozessklasse 8. Historyeintrag |
| STAT_HISTORY_8_SWIP_VERSION_WERT | - | - | string | - | - | - | - | - | Angabe der Version der Prozessklasse 8. Historyeintrag |
| STAT_HISTORY_8_NEW_SW_VID_WERT | - | - | string | - | - | - | - | - | Neue Steuergeräte Software Version ID  Beispiel:    SD-B71200;TE-0A12B7-B712;MP-0A12C3-B712;PI-0A1001-B712 8. Historyeintrag |
| STAT_HISTORY_8_FLASHSPEICHER_WERT | kBytes | - | string | - | - | - | - | - | Freier Flashspeicher, der für Updates nach dem Update zur Verfügung steht (0xff ff ff ff wenn unbekannt) 8. Historyeintrag |
| STAT_HISTORY_8_ERROR_CODE | 0-n | - | unsigned char | - | TSoftwareUpdateErrorCode | - | - | - | Software Update Fehlercode 8. Historyeintrag |

<a id="table-tsoftwareupdatetyp"></a>
### TSOFTWAREUPDATETYP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | USB Installation |
| 0x01 | OTA Installation |
| 0x04 | Auto-Reinstallation |
| 0x05 | Entfernen des letzten Update |
| 0x06 | Entfernen aller Benutzerupdates per Diagnose |
| 0xFF | undefiniert |

<a id="table-tsoftwareupdateerrorcode"></a>
### TSOFTWAREUPDATEERRORCODE

Dimensions: 44 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Fahrzeug während Update nicht in Stillstand |
| 0x02 | Update Abbruch |
| 0x03 | MOST Kommunikationsfehler |
| 0x04 | SWUP Quelle antwortet nicht |
| 0x05 | Gerät ausgelastet |
| 0x0F | Unspezifizierter Umwelt-Fehler |
| 0x10 | Neueste Version schon installiert |
| 0x11 | SWUP Package Container veraltet |
| 0x1F | Unspezifizierter Versions-Fehler |
| 0x20 | Neue I-Stufe nötig |
| 0x21 | SWUP - Zielgerät nicht verfügbar |
| 0x22 | Abhängigkeiten nicht erfüllt |
| 0x23 | Betroffene SWE nicht gefunden |
| 0x24 | Pre-Installation Skripte Fehler |
| 0x25 | Post-Installation Skripte Fehler |
| 0x26 | Fahrgestellnummer stimmt nicht |
| 0x2F | Unspezifizierbarer Fehler: Updatekompatibiliät |
| 0x30 | SWUP Weiterleitung nicht unterstützt |
| 0x31 | Nicht genug RAM |
| 0x32 | Nicht genug Flashspeicher |
| 0x33 | System überlastet |
| 0x34 | SWUP-Paket zu groß |
| 0x3F | Unspezifizierbarer Fehler: Ressourcebeschränkungen |
| 0x40 | SWIP Signaturverifikation fehlgeschlagen |
| 0x41 | SWIP XML-Datei korrupt |
| 0x42 | SWUP Hash Value stimmt nicht |
| 0x43 | SGBM korrupt oder unerwartetes Format |
| 0x44 | SWUP Signaturverifikation fehlgeschlagen |
| 0x4F | Unspezifizierter Fehler: Integrität oder Authentisierung |
| 0x50 | SWUP Download abgebrochen |
| 0x5F | Unspezifizierter Over-The-Air-Fehler |
| 0x60 | Keine Deinstallationinformationen verfügbar |
| 0x61 | Pre-Deinstallation Skripte Fehler |
| 0x62 | Post-Deinstallation Skripte Fehler |
| 0x6F | Unspezifierter Deinstallationfehler |
| 0x70 | Keine Update-Datei verfügbar |
| 0x71 | Update läuft |
| 0x72 | USB Gerät nicht angeschlossen |
| 0x7F | Unspezifierter Betriebsystemfehler |
| 0xE0 | Speicher oder Filesystem defekt |
| 0xE1 | Inkonsistenter System Status |
| 0xEF | Unspezifierter Systemdefekt oder inkonsistenter Systemstatus |
| 0xFF | Unspezifizierter Fehler |

<a id="table-res-0xd035"></a>
### RES_0XD035

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SIM_STATUS | 0-n | high | unsigned int | - | TSimStatus | - | - | - | Status der SIM-Karte |
| STAT_IP_ADRESSE_WERT | - | high | string | - | - | - | - | - | IP-Adresse z.B. 192.168.0.1 |

<a id="table-arg-0xd035"></a>
### ARG_0XD035

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DEVICE | 0-n | - | int | - | TLastConnectionTel | - | - | - | - | - | Argument beschreibt welches Gerät für das die letze Verbindung abgefragt wird. 1: Bluetooth Telefon 2: internes NAD Modul |

<a id="table-tlastconnectiontel"></a>
### TLASTCONNECTIONTEL

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Bluetooth |
| 0x02 | NAD |

<a id="table-tsimstatus"></a>
### TSIMSTATUS

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xff | undefinierter Status |
| 0x00 | nicht eingebucht, sucht kein Netz |
| 0x01 | eingebucht |
| 0x02 | nicht eingebucht, sucht ein Netz |
| 0x03 | einbuchen verweigert |
| 0x04 | eingebucht und roaming |
| 0x05 | eingebucht und roaming off-net |
| 0x10 | Emergency Call bereit |

<a id="table-res-0xd047"></a>
### RES_0XD047

Dimensions: 65 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NUMBER_OF_ENTRIES_WERT | - | - | int | - | - | - | - | - | Anzahl der Elemente in der Historie |
| STAT_SRVC_APPLICATION_ID_1 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_1_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_1_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_1 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_2 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_2_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_2_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_2 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_3 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_3_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_3_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_3 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_4 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_4_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_4_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_4 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_5 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_5_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_5_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_5 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_6 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_6_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_6_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_6 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_7 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_7_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_7_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_7 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_8 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_8_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_8_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_8 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_9 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_9_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_9_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_9 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_10 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_10_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_10_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_10 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_11 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_11_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_11_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_11 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_12 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_12_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_12_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_12 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_13 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_13_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_13_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_13 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_14 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_14_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_14_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_14 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_15 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_15_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_15_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_15 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |
| STAT_SRVC_APPLICATION_ID_16 | 0-n | - | char | - | TRemoteServices | - | - | - | Gibt die eindeutige ID des angefragten Remote Services an , x steht für die fortlaufende Nummer in der Historie |
| STAT_SRVC_SEND_TIME_16_WERT | - | - | string | - | - | - | - | - | Wann ist der Trigger in der Combox angekommen, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_EXEC_TIME_16_WERT | - | - | string | - | - | - | - | - | Wann hat die Applikation Remote Services die Nachricht auf den MST gelegt, TT/mm/jjjj hh:mm:ss |
| STAT_SRVC_DOORS_STATUS_16 | 0-n | - | char | - | TDoorsStatus | - | - | - | 0x00 wenn mind. 1 Tür nicht verschlossen ist, 0x01 wenn alle Türen UND die Heckklappe verschlossen sind |

<a id="table-tremoteservices"></a>
### TREMOTESERVICES

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Remote Door (Lock or Unlock)  |
| 0x01 | Remote Climate Control |
| 0x02 | Vehicle Finder (incl. Flash Light and / or Horn Blow)  |
| 0xFF | undefinierter Zustand |

<a id="table-tdoorsstatus"></a>
### TDOORSSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | mindestens 1 Tür nicht verschlossen |
| 0x01 | alle Türen UND Heckklappe verschlossen |
| 0xFF | undefinierter Zustand |

<a id="table-res-0xd057"></a>
### RES_0XD057

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_USB_HUB_TEST_PORT_1 | 0-n | - | unsigned char | - | THubConnectionState | - | - | - | Status HUB Verbindung Port 1 |
| STAT_USB_HUB_TEST_PORT_2 | 0-n | - | unsigned char | - | THubConnectionState | - | - | - | Status HUB Verbindung Port 2 |

<a id="table-thubconnectionstate"></a>
### THUBCONNECTIONSTATE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | HUB angeschlossen |
| 0x01 | HUB nicht angeschlossen |
| 0x04 | HUB nicht codiert |
| 0xFF | nicht definiert |

<a id="table-tab-tdaactivationstate"></a>
### TAB_TDAACTIVATIONSTATE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Leerlauf, derzeit nicht aktiv |
| 0x02 | Aktivierung läuft |
| 0x03 | Aktivierung fehlgeschlagen |
| 0x04 | Aktivierung erfolgreich |
| 0xFF | nicht definiert |

<a id="table-res-0xd099"></a>
### RES_0XD099

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_USB_KDZ | 0-n | high | unsigned long | - | - | - | - | - | Anzahl der Steckzyklen am USB Interface |
| STAT_USB_SIA | 0-n | high | unsigned long | - | - | - | - | - | Anzahl der Steckzyklen am SIA Interface |

<a id="table-res-0xa019"></a>
### RES_0XA019

Dimensions: 35 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | gibt an, welche externen Anschlüsse getestet wurden. |
| STAT_TEST_AUXVERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TTestStatus | - | - | - | Gibt den Status des gesamten Tests oder der entsprechenden Anschlüsse wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. |
| STAT_ANZAHL_FEHLERHAFTE_VERBINDUNGEN_WERT | - | - | + | - | - | unsigned char | - | - | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 2 oder 3 meldet. Gibt wieder, wie viele Fehler während des Tests gefunden wurden. |
| STAT_FEHLER_1_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_1_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_2_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_2_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_3_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_3_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_4_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_4_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_5_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_5_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_6_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_6_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_7_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_7_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_8_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_8_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_9_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_9_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_10_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_10_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_11_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_11_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_12_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_12_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_13_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_13_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_14_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_14_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_15_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_15_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_16_VERBINDUNG | - | - | + | 0-n | - | unsigned int | - | TAuxVerbindung | - | - | - | Gibt den Anschluss wieder, bei dem der Fehler X auftrat. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |
| STAT_FEHLER_16_FEHLERART_VERBINDUNG | - | - | + | 0-n | - | unsigned char | - | TVerbindungFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOEINGANG nicht den Wert 3 (Fehler) meldet. Wert Text:  0 Kurzschluss nach Plus,  1 Kurzschluss nach Masse,  2 Leitungsunterbrechung,  255 Nicht definiert.  Dieses Result wird mit 255 belegt, wenn STAT_TEST_AUXVERBINDUNG nicht den Wert 3 (Fehler) meldet oder die Auxverbindung nicht existiert. |

<a id="table-arg-0xa019"></a>
### ARG_0XA019

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_VERBINDUNG | + | - | - | - | unsigned int | - | - | - | - | - | - | - | legt den externen Anschluss fest, der getestet werden soll. Bei Angabe des Wertes 0 werden alle vorhandenen und schaltbaren Anschlüsse nacheinander getestet. Alle steuerbaren Anschlüsse des Steuergerätes müssen einzeln und kombiniert testbar sein. Tabelle TAuxVerbindung |

<a id="table-tauxverbindung"></a>
### TAUXVERBINDUNG

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Aux Verbindungen |
| 0x0001 | Aux In Audio |
| 0x0100 | Aux In RSE links |
| 0x0200 | Aux In RSE rechts |
| 0x0400 | Aux In RSE BMW Individual |
| 0xFFFF | Nicht definiert |

<a id="table-tverbindungfehlerart"></a>
### TVERBINDUNGFEHLERART

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0xFF | Nicht definiert |

<a id="table-res-0xa022"></a>
### RES_0XA022

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SELBSTTEST_ROUTINE | - | - | + | 0-n | - | unsigned long | - | TSelbsttestRoutine | - | - | - | Routine(n), die getestet wurde(n). Tabelle  TSelbsttestRoutine |
| STAT_SELBSTTEST | - | - | + | 0-n | - | unsigned char | - | TTestStatus | - | - | - | Gibt den Status des Tests wieder. |

<a id="table-arg-0xa022"></a>
### ARG_0XA022

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_SELBSTTEST_ROUTINE | + | - | - | - | unsigned long | - | - | - | - | - | - | - | Routinen, die getestet werden sollen. Die Tabelle TSelbsttestRoutine wird in der SGBD von der Entwicklung bzw. vom Zulieferer befüllt und gepflegt. |

<a id="table-tselbsttestroutine"></a>
### TSELBSTTESTROUTINE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Routinen |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-res-0xa046"></a>
### RES_0XA046

Dimensions: 3 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PROVISIONING | - | - | + | 0-n | - | unsigned char | - | TProvisioningStatusTel | - | - | - | Status des Provisionierungsprozess Werte gemäß Tabelle TProvisioningStatusTel |
| STAT_MB_OTA_ID_WERT | - | - | + | - | - | string | - | - | - | - | - | Version von den aktuellen OTA Daten |
| STAT_MB_DAS_ID_WERT | - | - | + | - | - | string | - | - | - | - | - | Version von den aktuellen DAS Daten |

<a id="table-tprovisioningstatustel"></a>
### TPROVISIONINGSTATUSTEL

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | unbekannt |
| 0x01 | läuft noch |
| 0x02 | alles OK |
| 0x03 | mit Fehler beendet |
| 0x04 | wurde nicht gestartet |
| 0xFF | nicht definiert |

<a id="table-res-0xa048"></a>
### RES_0XA048

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT | - | - | + | 0-n | - | unsigned char | - | TBluetoothStatus | - | - | - | Liest den Bluetooth Status aus |

<a id="table-arg-0xa048"></a>
### ARG_0XA048

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT | + | - | 0-n | - | unsigned char | - | TBluetoothStatus | - | - | - | - | - | Setzt den Bluetooth Status |

<a id="table-tbluetoothstatus"></a>
### TBLUETOOTHSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bluetooth nicht aktiviert |
| 1 | Bluetooth aktiviert |
| 0xFF | nicht definiert |

<a id="table-res-0xa049"></a>
### RES_0XA049

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BT_ERKENNUNGSMODUS | - | - | + | 0-n | - | unsigned char | - | TBluetoothDiscoveryModeStatus | - | - | - | Liest den Status des Bluetooth Erkennungsmodus |

<a id="table-arg-0xa049"></a>
### ARG_0XA049

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_BT_ERKENNUNGSMODUS | + | - | 0-n | - | unsigned char | - | TBluetoothDiscoveryModeStatus | - | - | - | - | - | Steuert den Bluetooth Erkennungsmodus |

<a id="table-tbluetoothdiscoverymodestatus"></a>
### TBLUETOOTHDISCOVERYMODESTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | BT Erkennungsmodus aus |
| 1 | BT Erkennungsmodus ein |
| 0xFF | nicht definiert |

<a id="table-res-0xa04c"></a>
### RES_0XA04C

Dimensions: 6 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_JOB_RESULT | - | - | + | 0-n | - | unsigned char | - | TBluetoothReset | - | - | - | Allgemeiner Status Report |
| STAT_PAIRED_DEVICE_DELETED | - | - | + | 0-n | - | unsigned char | - | TBluetoothReset | - | - | - | Status Löschen Telefonbücher und Gesprächslisten |
| STAT_EMAIL_DELETED | - | - | + | 0-n | - | unsigned char | - | TBluetoothReset | - | - | - | Status Löschen E-Mails |
| STAT_SMS_DELETED | - | - | + | 0-n | - | unsigned char | - | TBluetoothReset | - | - | - | Status Löschen SMS |
| STAT_MUSIC_LIST_DELETED | - | - | + | 0-n | - | unsigned char | - | TBluetoothReset | - | - | - | Status Löschen Music List |
| STAT_PIM_DELETED | - | - | + | 0-n | - | unsigned char | - | TBluetoothReset | - | - | - | Status Löschen PIM |

<a id="table-arg-0xa04c"></a>
### ARG_0XA04C

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_DATA_TO_RESET | + | - | 0-n | - | unsigned long | - | TBluetoothResetBasicState | - | - | - | - | - | Löschen persönlicher Informationen  Liste der gekoppelten Geräte beinhaltet auch Gespächslisten und Sprachaufnahmen |

<a id="table-tbluetoothreset"></a>
### TBLUETOOTHRESET

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OK |
| 0x01 | Fehler aufgetreten |
| 0x02 | nicht angefordert |
| 0x03 | läuft gerade |
| 0xFF | nicht definiert |

<a id="table-tbluetoothresetbasicstate"></a>
### TBLUETOOTHRESETBASICSTATE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | alle |
| 0x0001 | Liste_gekoppelte_Geräte |
| 0x0002 | EMail |
| 0x0004 | SMS |
| 0x0008 | Musiklists |
| 0x0010 | PIM |
| 0x0020 | XX (vorgehalten) |
| 0x0040 | Musiksammlung |
| 0x0080 | Musiksammlung administrative Datenbanken |

<a id="table-res-0xa04f"></a>
### RES_0XA04F

Dimensions: 51 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt an, welche Antenne(n) getestet wurden. |
| STAT_TEST_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TTestStatus | - | - | - | Gibt den Status des gesamten Tests oder der entsprechenden Antennen wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. |
| STAT_ANZAHL_FEHLERHAFTE_ANTENNEN_WERT | - | - | + | - | - | unsigned char | - | - | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 2 oder 3 meldet. Gibt wieder, wie viele Fehler während des Tests gefunden wurden. |
| STAT_FEHLER_1_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | Rückgabe der Antenne, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_1_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_1_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_2_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_2_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_2_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_3_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_3_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_3_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_4_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_4_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_4_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_5_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_5_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_5_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_6_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_6_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_6_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_7_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_7_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_7_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_8_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_8_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_8_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_9_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_9_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_9_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_10_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_10_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_10_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_11_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_11_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_11_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_12_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_12_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_12_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_13_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_13_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_13_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_14_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_14_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_14_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_15_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_15_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_15_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |
| STAT_FEHLER_16_ANTENNE | - | - | + | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_16_FEHLERART_ANTENNE | - | - | + | 0-n | - | unsigned char | - | TAntenneFehlerArt | - | - | - | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_16_MESSWERT_WIDERSTAND_WERT | - | - | + | 0,1kOhm | - | unsigned int | - | - | - | - | - | der auf der fehlerhaften Antenne X gemessene Widerstand in 0.1 kOhm. |

<a id="table-arg-0xa04f"></a>
### ARG_0XA04F

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_ANTENNE | + | - | 0-n | - | unsigned long | - | TAntenneCMEDIA | - | - | - | 0.0 | - | Antenne(n) die getestet werden sollen. Tabelle TAntenneCMEDIA |

<a id="table-tantennecmedia"></a>
### TANTENNECMEDIA

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle |
| 0x00000001 | Bluetooth |
| 0xFFFFFFFF | nicht definiert |

<a id="table-tantennefehlerart"></a>
### TANTENNEFEHLERART

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | Falscher Antennfuß oder Diversity |
| 0xFF | Nicht definiert |

<a id="table-res-0xa050"></a>
### RES_0XA050

Dimensions: 2 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VERBAU_ROUTINE | - | - | + | 0-n | - | unsigned long | - | TVerbauCMEDIA | - | - | - | Ausgeführte Testroutine(n). |
| STAT_TEST_VERBAU | - | - | + | 0-n | - | unsigned char | - | TTestStatus | - | - | - | Gibt den Status des Verbautests wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. |

<a id="table-arg-0xa050"></a>
### ARG_0XA050

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ARG_VERBAU_ROUTINE | + | - | - | - | unsigned long | - | - | - | - | - | - | - | Routinen, die getestet werden sollen. Tabelle TVerbauCMEDIA |

<a id="table-tverbaucmedia"></a>
### TVERBAUCMEDIA

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle |
| 0x00000001 | Bluetooth |
| 0x00000008 | Ethernet |
| 0x00000010 | AuxIn |
| 0x00000020 | Mikrophon1 |
| 0x00000040 | Mikrophon2 |
| 0xFFFFFFFF | nicht definiert |

<a id="table-tteststatus"></a>
### TTESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft |
| 0x02 | Test beendet ohne Fehler |
| 0x03 | Test beendet mit Fehlern |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-res-0xa05a"></a>
### RES_0XA05A

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REMOVE_CUSTOMER_UPDATES | - | - | + | 0/1 | - | char | - | - | - | - | - | Entfernen aller Benutzer Updates; 0: nicht erfolgreich 1: erfolgreich |

<a id="table-res-0xa079"></a>
### RES_0XA079

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RESET_TO_DEFAULT_CONFIG | - | - | + | 0-n | - | unsigned char | - | TResetStatus | - | - | - | Status Reset Werte gemäß Tabelle TResetStatus 0 UNKNOWN - unbekannt 1 ACTIVE - läuft noch 2 SUCCESS - alles OK 3 FAILED - mit Fehler beendet 4 IDLE - wurde nicht gestartet |

<a id="table-tresetstatus"></a>
### TRESETSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | unbekannt |
| 0x01 | läuft noch |
| 0x02 | alles OK |
| 0x03 | mit Fehler |
| 0x04 | wurde nicht gestartet |
| 0xFF | undefinierter Zustand |

<a id="table-res-0xf015"></a>
### RES_0XF015

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEST | - | - | + | 0-n | high | unsigned char | - | TA4ASTRINGSTATUS | - | - | - | Status of the string is present or not |

<a id="table-ta4astringstatus"></a>
### TA4ASTRINGSTATUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | String present |
| 0x01 | String not present |

<a id="table-tsoftwareupdateprozessklasse"></a>
### TSOFTWAREUPDATEPROZESSKLASSE

Dimensions: 22 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ungültige SGBM-ID |
| 0x01 | Hardware (Elektronik) (HWEL) |
| 0x02 | Hardwareausprägung (HWAP) |
| 0x03 | Hardwarefarbe (HWFR) |
| 0x05 | Codierdaten (CAFD) |
| 0x06 | Bootloader (BTLD) |
| 0x07 | Flashloader Slave (FLSL) |
| 0x08 | Software ECU-Speicherimage (SWFL) |
| 0x09 | Flash File Software (SWFF) |
| 0x0A | Prüfsoftware (SWPF) |
| 0x0B | Programmiersystem (ONPS) |
| 0x0C | Interaktive Betriebsanleitung Daten (IBAD) |
| 0x0F | FA2FP (FAFP) |
| 0x10 | Freischaltcode Fahrzeugauftrag (FCFA) |
| 0x1A | Temporäre Lösch Routine (TLRT) |
| 0x1B | Temporäre Programmier Routine (TPRG) |
| 0xA0 | Entertainment Daten (ENTD) |
| 0xA1 | Navigation Daten (NAVD) |
| 0xA2 | Freischaltcode Funktion (FCFN) |
| 0xC0 | Software Update Package (SWUP) |
| 0xC1 | SWUP Index Package (SWIP) |
| 0xFF | Ungültige SGBM-ID |

<a id="table-tpowerstate"></a>
### TPOWERSTATE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Default; This state should never be logged |
| 0x01 | Sleepmode |
| 0x02 | Bus Active (Normal Operation, light on) |
| 0x03 | Local Active (Normal Operation, light off) |
| 0x04 | Shut-Down |
| 0x05 | Start-Up |
| 0xFF | Nicht definiert |

<a id="table-tpowerevent"></a>
### TPOWEREVENT

Dimensions: 23 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | No change |
| 0x01 | Most Light on |
| 0x02 | Most Light off |
| 0x03 | RST received |
| 0x04 | Sleepmode command received |
| 0x07 | Start-Up OK (First-Switch-To-Power) |
| 0x08 | Timeout |
| 0x09 | Temperature Shut-Down (Over Temperature detected) |
| 0x0A | Under voltage detected |
| 0x0B | Shutdown.Query Received |
| 0x0C | Clamp Off |
| 0x14 | SW Reset |
| 0x15 | Request by Coding (Diagnostic reset) |
| 0x16 | Watchdog Reset |
| 0x28 | Request Subnetwork |
| 0x29 | Telematic active |
| 0x2A | Telematic inactive |
| 0x2B | Phone Call active |
| 0x2C | Phone Call inactive |
| 0x3C | Shut-Down Reclaiming started |
| 0x3D | Shut-Down Reclaiming stopped |
| 0x3E | Shut-Down interrupted (Light On during Shut-Down) |
| 0xFF | Nicht definiert |
