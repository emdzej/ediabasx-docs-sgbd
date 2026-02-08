# FLM02_L.prg

- Jobs: [38](#jobs)
- Tables: [108](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Frontlichtmodul links |
| ORIGIN | BMW EK-722 Viktor_Rack |
| REVISION | 2.200 |
| AUTHOR | LEAR-CORPORATION-GMBH EK-522 Huhn |
| COMMENT | Zufügen funktionaler DTCs |
| PACKAGE | 1.90 |
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
- [IS_LESEN](#job-is-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $17 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $18 reportDTCSnapshotRecordByDTCNumber UDS  : $19 reportDTCExtendedDataRecordByDTCNumber UDS  : $-- reportSeverityInformationOfDTC (nicht möglich!) Modus: Default
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
- [STATUS_SATELLIT_DATEN](#job-status-satellit-daten) - Ausgabe der Logistikdaten Satellit mit HW-Version, SW-Version, BTLD-Version, Codierdaten-Checksumme Modus: Default
- [STATUS_SATELLIT_LASER_SICHERHEIT](#job-status-satellit-laser-sicherheit) - Gibt den Sicherheitsstatus des Lasers aus Modus: Default
- [STATUS_SATELLIT_FS_LESEN](#job-status-satellit-fs-lesen) - Ausgabe des internen Fehlerspeichers einer Satellitenelektronik Modus: Default
- [STATUS_SATELLIT_RESET_ZAEHLER](#job-status-satellit-reset-zaehler) - Gibt die Anzahl der Resets des Satelliten aus Modus: Default
- [STEUERN_SATELLIT_LASER_SICHERHEITSSTATUS_RESET](#job-steuern-satellit-laser-sicherheitsstatus-reset) - Ruecksetzen des Sicherheitsstatus des Lasersatelliten Modus: Default
- [STATUS_SATELLIT_LASER_KALIBRIERPARAMETER](#job-status-satellit-laser-kalibrierparameter) - Gibt die Kalibrierwerte des Lasersatelliten aus Modus: Default
- [STATUS_SATELLIT_LASER_PROGRAMMING_COUNTER](#job-status-satellit-laser-programming-counter) - Programmierzähler Lasersatellit Modus: Default

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

Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $17 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default

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

sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $18 reportDTCSnapshotRecordByDTCNumber UDS  : $19 reportDTCExtendedDataRecordByDTCNumber UDS  : $-- reportSeverityInformationOfDTC (nicht möglich!) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | gewaehlter Infocode |

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
| _REQUEST_SNAPSHOT | binary | Anfrage ans SG |
| _REQUEST_EXTENDED_DATA | binary | Anfrage ans SG |
| _RESPONSE_SNAPSHOT | binary | Hex-Antwort von SG |
| _RESPONSE_EXTENDED_DATA | binary | Hex-Antwort von SG |
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
| CPS | string | Codierpruefstempel bis SP2021 bestehend aus VIN7        7 Zeichen (ASCII) Codierpruefstempel ab SP2021 bestehend aus Codierdatum 6 Zeichen (3 Byte Hex) bestehend aus TesterNr    6 Zeichen (3 Byte Hex) bestehend aus LizenzID   10 Zeichen (5 Byte Hex) bestehend aus VIN7        7 Zeichen (ASCII) |
| CPS_VIN7 | string | 7 Zeichen (ASCII) |
| CPS_DATUM | string | erst ab SP2021 Codierdatum 8 Zeichen TT.MM.JJJJ |
| CPS_TESTERNR | string | erst ab SP2021 Tester-Nummer 6 Zeichen hex |
| CPS_LIZENZID | string | erst ab SP2021 Tester-Lizenz-ID 10 Zeichen hex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-satellit-daten"></a>
### STATUS_SATELLIT_DATEN

Ausgabe der Logistikdaten Satellit mit HW-Version, SW-Version, BTLD-Version, Codierdaten-Checksumme Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_SAT_1_HW_VERSION_DATA | string | HW Version Satellit 1 |
| STAT_SAT_1_BTLD_VERSION_DATA | string | BTLD Version Satellit 1 |
| STAT_SAT_1_SW_VERSION_DATA | string | SW Version Satellit 1 |
| STAT_SAT_1_CODIERDATEN_STATUS_WERT | char | Codierdaten Status-Wert Satellit 1 |
| STAT_SAT_1_CODIERDATEN_HASH_WERT | int | Codierdaten Hash-Wert Satellit 1 |
| STAT_SAT_1_VENDOR_ID_WERT | int | Codierdaten Hash-Wert Satellit 1 |

<a id="job-status-satellit-laser-sicherheit"></a>
### STATUS_SATELLIT_LASER_SICHERHEIT

Gibt den Sicherheitsstatus des Lasers aus Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_LSR_WERT | char | Sicherheitsstatus Laser |
| STAT_LSR_SENS_STAT_1_WERT | char | Sicherheitsstatus Laser Sensor 1 |
| STAT_LSR_SENS_STAT_2_WERT | char | Sicherheitsstatus Laser Sensor 2 |
| STAT_LSR_RETRIES_PER_TRIP_WERT | char | Anzahl Einschaltversuche pro Fahrzyklus |
| STAT_LSR_ERROR_WERT | char | Status Limit Anzahl Einschaltversuche pro Fahrzyklus |
| STAT_LSR_RETIRES_ABS_WERT | char | GesamtzÃ¤hler Einschaltversuche Laser |
| STAT_LSR_LOCK_WERT | char | Laser gesprerrt |
| STAT_LSR_SENS_1_MV_WERT | int | Rohwert Laser-Lichtsensor 1 |
| STAT_LSR_SENS_2_MV_WERT | int | Rohwert Laser-Lichtsensor 2 |
| STAT_LSR_SENS_1_WERT | long | Normierter Wert Laser-Lichtsensor 1 |
| STAT_LSR_SENS_2_WERT | long | Normierter Wert Laser-Lichtsensor 2 |
| STAT_LSR_AGE_MODE_WERT | char | Wert des Codierparameters SAT_LSR_SENS_AGEING_MODE |
| STAT_LSR_AGE_WERT | char | Laser Status Alterungsmodus |
| STAT_AGE_FACTOR_1_WERT | int | Kompensationsfaktor Alterung Laser Sensor 1 |
| STAT_AGE_FACTOR_2_WERT | int | Kompensationsfaktor Alterung Laser Sensor 2 |
| STAT_SAFETY_READ_ZKW_DATA | binary | Sicherheitsdaten Laser ZKW |

<a id="job-status-satellit-fs-lesen"></a>
### STATUS_SATELLIT_FS_LESEN

Ausgabe des internen Fehlerspeichers einer Satellitenelektronik Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_SAT_FSP_EINTRAG_1_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_2_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_3_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_4_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_5_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_6_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_7_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_8_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_9_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_10_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_11_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_12_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_13_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_14_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_15_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_16_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_17_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_18_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |
| STAT_SAT_FSP_EINTRAG_19_DATA | binary | FSP-Nummer Satellit inkl. Systemzeit, Fehlerstatus und Umweltbedingungen |

<a id="job-status-satellit-reset-zaehler"></a>
### STATUS_SATELLIT_RESET_ZAEHLER

Gibt die Anzahl der Resets des Satelliten aus Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_RESET_ZAEHLER_WERT | int | Hex-Antwort von SG |

<a id="job-steuern-satellit-laser-sicherheitsstatus-reset"></a>
### STEUERN_SATELLIT_LASER_SICHERHEITSSTATUS_RESET

Ruecksetzen des Sicherheitsstatus des Lasersatelliten Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-satellit-laser-kalibrierparameter"></a>
### STATUS_SATELLIT_LASER_KALIBRIERPARAMETER

Gibt die Kalibrierwerte des Lasersatelliten aus Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_LSR_BINNING_CLASS_WERT | char | Gibt die Binningklasse des Lasers aus |
| STAT_VTHR_OFFSET_1_WERT | int | Stromkalibrierung Offset Treiberkanal 1 |
| STAT_VTHR_OFFSET_2_WERT | int | Stromkalibrierung Offset Treiberkanal 2 |
| STAT_VTHR_FACTOR_1_WERT | int | Stromkalibrierung Faktor Treiberkanal 1 |
| STAT_VTHR_FACTOR_2_WERT | int | Stromkalibrierung Faktor Treiberkanal 2 |
| STAT_BUCK_TOFF_1_WERT | char | Kalibrierung T_OFF Konstante Treiberkanal 1 |
| STAT_BUCK_TOFF_2_WERT | char | Kalibrierung T_OFF Konstante Treiberkanal 2 |
| STAT_LSR0_1_WERT | char | Laser-Lichtsensor 1, Dunkelwert |
| STAT_LSR0_2_WERT | char | Laser-Lichtsensor 2, Dunkelwert |
| STAT_LSR100_1_WERT | char | Laser-Lichtsensor 1, 100%-Wert |
| STAT_LSR100_2_WERT | char | Laser-Lichtsensor 2, 100%-Wert |
| STAT_LSR_1P_M_I_WERT | char | normierter Faktor fÃ¼r Steigung zwischen IMin und IMax |
| STAT_LSR_1P_M_I0_WERT | char | normierte Steigung fÃ¼r T=0Â°C |
| STAT_LSR_1P_M_1T_WERT | char | normierte Steigung fÃ¼r I=Imin |
| STAT_LSR_1P_X_R_10_WERT | char | normierter erwarteter korrigierter Rohwert fÃ¼r I=IMin und T=0Â°C |
| STAT_I_N_WERT | char | Nennstrom |
| STAT_T_N_WERT | char | Nenntemperatur |

<a id="job-status-satellit-laser-programming-counter"></a>
### STATUS_SATELLIT_LASER_PROGRAMMING_COUNTER

Programmierzähler Lasersatellit Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_PROGRAMMING_COUNTER_ACT_WERT | int | aktueller Wert Programming Counters |
| STAT_PROGRAMMING_COUNTER_MAX_WERT | int | maximaler Wert Programming Counters |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (142 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (7 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [ARG_0X4044_D](#table-arg-0x4044-d) (1 × 12)
- [ARG_0X4045_D](#table-arg-0x4045-d) (4 × 12)
- [ARG_0X404C_D](#table-arg-0x404c-d) (10 × 12)
- [ARG_0X404E_D](#table-arg-0x404e-d) (1 × 12)
- [ARG_0XA54B_R](#table-arg-0xa54b-r) (3 × 14)
- [ARG_0XA54C_R](#table-arg-0xa54c-r) (5 × 14)
- [ARG_0XA54D_R](#table-arg-0xa54d-r) (1 × 14)
- [ARG_0XA54E_R](#table-arg-0xa54e-r) (3 × 14)
- [ARG_0XA54F_R](#table-arg-0xa54f-r) (3 × 14)
- [ARG_0XA550_R](#table-arg-0xa550-r) (3 × 14)
- [ARG_0XAFF3_R](#table-arg-0xaff3-r) (3 × 14)
- [ARG_0XD6D4_D](#table-arg-0xd6d4-d) (1 × 12)
- [ARG_0XD6DC_D](#table-arg-0xd6dc-d) (2 × 12)
- [ARG_0XD7AB_D](#table-arg-0xd7ab-d) (1 × 12)
- [ARG_0XD7AC_D](#table-arg-0xd7ac-d) (1 × 12)
- [ARG_0XD7B9_D](#table-arg-0xd7b9-d) (1 × 12)
- [ARG_0XD7BB_D](#table-arg-0xd7bb-d) (1 × 12)
- [ARG_0XD7BD_D](#table-arg-0xd7bd-d) (1 × 12)
- [ARG_0XD9BE_D](#table-arg-0xd9be-d) (1 × 12)
- [ARG_0XD9FD_D](#table-arg-0xd9fd-d) (2 × 12)
- [ARG_0XDA72_D](#table-arg-0xda72-d) (1 × 12)
- [ARG_0XDAC5_D](#table-arg-0xdac5-d) (1 × 12)
- [ARG_0XE3ED_D](#table-arg-0xe3ed-d) (2 × 12)
- [ARG_0XF001_R](#table-arg-0xf001-r) (2 × 14)
- [ARG_0XF002_R](#table-arg-0xf002-r) (2 × 14)
- [BF_22_F152_SUPPLIERINFO](#table-bf-22-f152-supplierinfo) (2 × 10)
- [BF_FAHRZEUG_ENTWICKLUNGSBEZEICHNUNG](#table-bf-fahrzeug-entwicklungsbezeichnung) (2 × 10)
- [BF_FEHLERARTEN_SCHRITTMOTOR](#table-bf-fehlerarten-schrittmotor) (8 × 10)
- [BF_FEHLERARTEN_SCHRITTMOTOR_AHL](#table-bf-fehlerarten-schrittmotor-ahl) (8 × 10)
- [BF_LED_KANAL](#table-bf-led-kanal) (3 × 10)
- [BF_SCHEINWERFER_TYP](#table-bf-scheinwerfer-typ) (4 × 10)
- [BITFELD](#table-bitfeld) (18 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FAHRZEUG_TYP](#table-fahrzeug-typ) (43 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (213 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (23 × 9)
- [HW_MODEL](#table-hw-model) (5 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (42 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (10 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [RDBI_ADS_DOP](#table-rdbi-ads-dop) (10 × 2)
- [RDBI_PC_PCS_DOP](#table-rdbi-pc-pcs-dop) (4 × 2)
- [REFERENZIERUNG_SCHRITTMOTOR](#table-referenzierung-schrittmotor) (4 × 2)
- [RES_0X2502_D](#table-res-0x2502-d) (3 × 10)
- [RES_0X2504_D](#table-res-0x2504-d) (6 × 10)
- [RES_0X4040_D](#table-res-0x4040-d) (2 × 10)
- [RES_0X4041_D](#table-res-0x4041-d) (2 × 10)
- [RES_0X4042_D](#table-res-0x4042-d) (2 × 10)
- [RES_0X4046_D](#table-res-0x4046-d) (59 × 10)
- [RES_0X4047_D](#table-res-0x4047-d) (48 × 10)
- [RES_0X4048_D](#table-res-0x4048-d) (6 × 10)
- [RES_0X4049_D](#table-res-0x4049-d) (18 × 10)
- [RES_0X404B_D](#table-res-0x404b-d) (11 × 10)
- [RES_0X404D_D](#table-res-0x404d-d) (3 × 10)
- [RES_0X4051_D](#table-res-0x4051-d) (2 × 10)
- [RES_0XA549_R](#table-res-0xa549-r) (34 × 13)
- [RES_0XA54A_R](#table-res-0xa54a-r) (1 × 13)
- [RES_0XA54C_R](#table-res-0xa54c-r) (1 × 13)
- [RES_0XA54D_R](#table-res-0xa54d-r) (48 × 13)
- [RES_0XA54E_R](#table-res-0xa54e-r) (1 × 13)
- [RES_0XA54F_R](#table-res-0xa54f-r) (1 × 13)
- [RES_0XAFF3_R](#table-res-0xaff3-r) (10 × 13)
- [RES_0XD6D3_D](#table-res-0xd6d3-d) (7 × 10)
- [RES_0XD6DB_D](#table-res-0xd6db-d) (60 × 10)
- [RES_0XD6DF_D](#table-res-0xd6df-d) (12 × 10)
- [RES_0XD7A7_D](#table-res-0xd7a7-d) (48 × 10)
- [RES_0XD7AD_D](#table-res-0xd7ad-d) (38 × 10)
- [RES_0XD7BA_D](#table-res-0xd7ba-d) (14 × 10)
- [RES_0XD7BC_D](#table-res-0xd7bc-d) (2 × 10)
- [RES_0XD7BE_D](#table-res-0xd7be-d) (2 × 10)
- [RES_0XD9BD_D](#table-res-0xd9bd-d) (2 × 10)
- [RES_0XD9BF_D](#table-res-0xd9bf-d) (96 × 10)
- [RES_0XD9C8_D](#table-res-0xd9c8-d) (12 × 10)
- [RES_0XD9F6_D](#table-res-0xd9f6-d) (3 × 10)
- [RES_0XD9F7_D](#table-res-0xd9f7-d) (3 × 10)
- [RES_0XD9F8_D](#table-res-0xd9f8-d) (45 × 10)
- [RES_0XD9F9_D](#table-res-0xd9f9-d) (45 × 10)
- [RES_0XD9FA_D](#table-res-0xd9fa-d) (2 × 10)
- [RES_0XD9FB_D](#table-res-0xd9fb-d) (2 × 10)
- [RES_0XD9FC_D](#table-res-0xd9fc-d) (69 × 10)
- [RES_0XDA71_D](#table-res-0xda71-d) (6 × 10)
- [RES_0XDA72_D](#table-res-0xda72-d) (1 × 10)
- [RES_0XDAC8_D](#table-res-0xdac8-d) (3 × 10)
- [RES_0XE3EE_D](#table-res-0xe3ee-d) (14 × 10)
- [RES_0XF001_R](#table-res-0xf001-r) (1 × 13)
- [RES_0XF152_D](#table-res-0xf152-d) (2 × 10)
- [SCHEINWERFER_HERSTELLER](#table-scheinwerfer-hersteller) (5 × 2)
- [SCHEINWERFER_LAENDER_VARIANTE](#table-scheinwerfer-laender-variante) (3 × 2)
- [SCHEINWERFER_SA_VARIANTE](#table-scheinwerfer-sa-variante) (8 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (67 × 16)
- [TAB_FLM_HIGHSIDE_SWITCH](#table-tab-flm-highside-switch) (5 × 2)
- [TAB_FLM_KANAL_ARG](#table-tab-flm-kanal-arg) (16 × 2)
- [TAB_LF_LV_FRONT_ARG](#table-tab-lf-lv-front-arg) (78 × 2)
- [TAB_SUPPLIERINFO_FIELD](#table-tab-supplierinfo-field) (64 × 2)

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

Dimensions: 142 rows × 2 columns

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

<a id="table-arg-0x4044-d"></a>
### ARG_0X4044_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ID | HEX | high | signed char | - | - | - | - | - | - | - | ID des Schrittmotorausgangs 0=LWR, 1=AHL |

<a id="table-arg-0x4045-d"></a>
### ARG_0X4045_D

Dimensions: 4 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ID | HEX | high | signed char | - | - | - | - | - | - | - | ID des Schrittmotors, 0=LWR, 1=AHL |
| SCHRITTE | Schritte | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | - | - | Anzahl der zu fahrenden Schritte |
| RICHTUNG | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Richtung in die der Motor verfahren soll. 0: LWR direction 0 1: LWR direction 1 |
| ZEIT_PRO_SCHRITT | µs | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | - | - | Zeit in Mikrosekunden pro Schritt |

<a id="table-arg-0x404c-d"></a>
### ARG_0X404C_D

Dimensions: 10 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LED_CURRENT_0 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_1 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_2 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_3 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_4 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_5 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_6 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_7 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_8 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |
| LED_CURRENT_9 | mA | high | signed int | - | - | 1.0 | 1.0 | 0.0 | - | - | gibt den einzustellenden Strom des im Namen genannten LED-Kanals an |

<a id="table-arg-0x404e-d"></a>
### ARG_0X404E_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ACTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00: Löschen der Informationen des letzten Fusi-Resets durchführen 0x01: Löschen der Informationen des letzten Fusi-Resets durchführen |

<a id="table-arg-0xa54b-r"></a>
### ARG_0XA54B_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KANAL | + | - | 0-n | high | unsigned char | - | TAB_FLM_KANAL_ARG | - | - | - | - | - | Auswahl des FLM Kanal bzw. LED-Ausgang |
| PWM | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | PWM Wert |
| ZEIT | + | - | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der Aktivierungszeit in Sekunden. (255...dauerhaft ein) |

<a id="table-arg-0xa54c-r"></a>
### ARG_0XA54C_R

Dimensions: 5 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ADRESSE_SATELLIT | + | - | HEX | high | unsigned char | - | - | - | - | - | - | - | Auswahl der Satelliten-Adresse |
| SERVICE_ID | + | - | HEX | high | unsigned char | - | - | - | - | - | - | - | Auswahl der UDS Service-ID |
| DID_RID | + | - | HEX | high | unsigned char | - | - | - | - | - | - | - | Auswahl des DID bzw. RID Satellit |
| SUBFUNCTION_ID | + | - | HEX | high | unsigned char | - | - | - | - | - | - | - | Auswahl der Subfunction-ID Satellit |
| ARGUMENT | + | - | HEX | high | unsigned long | - | - | - | - | - | - | - | Argument für WriteData in den Satelliten |

<a id="table-arg-0xa54d-r"></a>
### ARG_0XA54D_R

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EINSCHALTDAUER_LUEFTER | + | - | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der Aktivierungszeit in Sekunden. (255...dauerhaft ein) |

<a id="table-arg-0xa54e-r"></a>
### ARG_0XA54E_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POSITION | + | - | ° | high | unsigned int | - | - | 100.0 | 1.0 | 2000.0 | - | - | Position des Schrittmotors in Grad |
| GESCHWINDIGKEIT | + | - | °/s | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | - | - | Verfahrgeschwindigkeit des Schrittmotors in Grad pro Sekunde |
| ZEIT | + | - | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der Aktivierungszeit in Sekunden. (255...dauerhaft ein) |

<a id="table-arg-0xa54f-r"></a>
### ARG_0XA54F_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POSITION | + | - | ° | high | unsigned int | - | - | 100.0 | 1.0 | 2000.0 | - | - | Position des Schrittmotors in Grad |
| GESCHWINDIGKEIT | + | - | °/s | high | unsigned char | - | - | 10.0 | 1.0 | 0.0 | - | - | Verfahrgeschwindigkeit des Schrittmotors in Grad pro Sekunde |
| ZEIT | + | - | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der Aktivierungszeit in Sekunden. (255...dauerhaft ein) |

<a id="table-arg-0xa550-r"></a>
### ARG_0XA550_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUGANG | + | - | 0-n | high | unsigned char | - | TAB_FLM_HIGHSIDE_SWITCH | - | - | - | - | - | Ausgang des Highside-Schalters. |
| PWM | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | PWM Wert |
| ZEIT | + | - | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der Aktivierungszeit in Sekunden. (255...dauerhaft ein) 255 = dauerhaft ein |

<a id="table-arg-0xaff3-r"></a>
### ARG_0XAFF3_R

Dimensions: 3 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BITCODE_KURZSCHLUSS_SCHALTER | + | - | HEX | high | signed int | - | - | - | - | - | - | - | Gibt an, welche KSS bitcodiert beeinflusst werden sollen. |
| PWM | + | - | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | 0.0 | 100.0 | Angabe der PWM Duty Cycle in % |
| ZEIT | + | - | s | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der Aktivierungszeit in Sekunden. (255...dauerhaft ein) |

<a id="table-arg-0xd6d4-d"></a>
### ARG_0XD6D4_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Zähler löschen: 0: keine Aktion 1: Start |

<a id="table-arg-0xd6dc-d"></a>
### ARG_0XD6DC_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LICHTFUNKTION_LV | 0-n | - | signed int | - | TAB_LF_LV_FRONT_ARG | - | - | - | - | - | Auswahl siehe table TAB_LF_LV_FRONT_ARG |
| ZEIT | s | - | unsigned char | - | - | 1.0 | 1.0 | 0.0 | - | - | Vorgabe der Aktivierungszeit in Sekunden. (255...dauerhaft ein) |

<a id="table-arg-0xd7ab-d"></a>
### ARG_0XD7AB_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG | 0-n | high | unsigned char | - | TAB_FLM_HIGHSIDE_SWITCH | - | - | - | - | - | Auswahl des jeweiligen Highside Schalters Nr. |

<a id="table-arg-0xd7ac-d"></a>
### ARG_0XD7AC_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Zähler löschen:  0: keine Aktion  1: Start |

<a id="table-arg-0xd7b9-d"></a>
### ARG_0XD7B9_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Zähler löschen:  0: keine Aktion  1: Start |

<a id="table-arg-0xd7bb-d"></a>
### ARG_0XD7BB_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Zähler löschen:  0: keine Aktion  1: Start |

<a id="table-arg-0xd7bd-d"></a>
### ARG_0XD7BD_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Zähler löschen:  0: keine Aktion  1: Start |

<a id="table-arg-0xd9be-d"></a>
### ARG_0XD9BE_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AKTION | 0/1 | high | unsigned char | - | - | - | - | - | - | - | Speicher löschen:  0: keine Aktion  1: Start |

<a id="table-arg-0xd9fd-d"></a>
### ARG_0XD9FD_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHRITTMOTOR | HEX | high | unsigned char | - | - | - | - | - | - | - | 0x00: keine Aktion  0x01: AHL  0x02: LWR 0x03: beide Schrittmotoren |
| MODUS | HEX | high | unsigned char | - | - | - | - | - | - | - | 0x00: Referenzieren  0x01: Abstellposition anfahren |

<a id="table-arg-0xda72-d"></a>
### ARG_0XDA72_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHEINWERFER_DATEN | DATA | high | data[16] | - | - | 1.0 | 1.0 | 0.0 | - | - | Scheinwerferspezifische Daten |

<a id="table-arg-0xdac5-d"></a>
### ARG_0XDAC5_D

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HIGHSIDE_NR | HEX | high | unsigned char | - | - | - | - | - | - | - | Reset HSS Nr. 0x01: 1, 0x03: SBC, 0xFF: alle |

<a id="table-arg-0xe3ed-d"></a>
### ARG_0XE3ED_D

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHEINWERFERSEITE | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00: aktuelle Seite (Diagnoseadresse)  0x01: andere Seite (Diagnoseadresse) |
| BINNINGDATEN | DATA | high | data[5] | - | - | 1.0 | 1.0 | 0.0 | - | - | Binningdaten Leuchtmittel der gewählten Fahrzeugseite |

<a id="table-arg-0xf001-r"></a>
### ARG_0XF001_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LED_TREIBER_NR | + | - | HEX | high | unsigned char | - | - | - | - | - | - | - | Nummer des LED-Treibers |
| REGISTER_ADRESSE | + | - | HEX | high | unsigned char | - | - | - | - | - | - | - | Adresse des Treiber-Registers |

<a id="table-arg-0xf002-r"></a>
### ARG_0XF002_R

Dimensions: 2 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PASSWORT | - | + | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | - | - | Passwort |
| RESET_TYP | - | + | 0/1 | high | unsigned char | - | - | - | - | - | - | - | 0x00: Software-Reset 0x01: Power-On-Reset |

<a id="table-bf-22-f152-supplierinfo"></a>
### BF_22_F152_SUPPLIERINFO

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HWMODEL | 0-n | high | unsigned char | 0xC0 | HW_MODEL | - | - | - | hardware model |
| STAT_SUPPLIERINFOFIELD | 0-n | high | unsigned char | 0x3F | TAB_SUPPLIERINFO_FIELD | - | - | - | supplierInfo |

<a id="table-bf-fahrzeug-entwicklungsbezeichnung"></a>
### BF_FAHRZEUG_ENTWICKLUNGSBEZEICHNUNG

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FAHRZEUGLISTE | 0-n | high | unsigned char | 0xFE | FAHRZEUG_TYP | - | - | - | Gibt die Entwicklungsbezeichnung des Fahrzeugs aus |
| STAT_LCI | 0/1 | high | unsigned char | 0x01 | - | - | - | - | 0x00: NICHT_LCI 0x01: LCI |

<a id="table-bf-fehlerarten-schrittmotor"></a>
### BF_FEHLERARTEN_SCHRITTMOTOR

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OPEN_LOAD | 0/1 | high | unsigned char | 0x01 | - | - | - | - | 0x00: kein Fehler 0x01: Open Load |
| STAT_KURZSCHLUSS_UBAT | 0/1 | high | unsigned char | 0x02 | - | - | - | - | 0x00: kein Fehler 0x01: Kurzschluss nach UBat |
| STAT_KURZSCHLUSS_MASSE | 0/1 | high | unsigned char | 0x04 | - | - | - | - | 0x00: kein Fehler 0x01: Kurzschluss nach Masse |
| STAT_INTERNER_FEHLER | 0/1 | high | unsigned char | 0x08 | - | - | - | - | 0x00: kein Fehler 0x01: Treiberfehler |
| STAT_SCHRITTVERLUST | 0/1 | high | unsigned char | 0x10 | - | - | - | - | 0x00: kein Fehler 0x01: Schrittverlust |
| STAT_TEMPERATUR_WARNUNG | 0/1 | high | unsigned char | 0x20 | - | - | - | - | 0x00: kein Fehler 0x01: Warnung Übertemperatur |
| STAT_TEMPERATUR_ABSCHALTUNG | 0/1 | high | unsigned char | 0x40 | - | - | - | - | 0x00: kein Fehler 0x01: Abschaltung Übertemperatur |
| STAT_UNDERVOLTAGE | 0/1 | high | unsigned char | 0x80 | - | - | - | - | 0x00: kein Fehler 0x01: Unterspannungsfehler |

<a id="table-bf-fehlerarten-schrittmotor-ahl"></a>
### BF_FEHLERARTEN_SCHRITTMOTOR_AHL

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_OPEN_LOAD_AHL | 0/1 | high | unsigned char | 0x01 | - | - | - | - | 0x00: kein Fehler 0x01: Fehler vorhanden |
| STAT_KURZSCHLUSS_UBATT_AHL | 0/1 | high | unsigned char | 0x02 | - | - | - | - | 0x00: kein Fehler 0x01: Kurzschluss nach UBatt |
| STAT_KURZSCHLUSS_MASSE_AHL | 0/1 | high | unsigned char | 0x04 | - | - | - | - | 0x00: kein Fehler 0x01: Kurzschluss nach Masse |
| STAT_INTERNER_FEHLER_AHL | 0/1 | high | unsigned char | 0x08 | - | - | - | - | 0x00: kein Fehler 0x01: Treiberfehler |
| STAT_SCHRITTVERLUST_AHL | 0/1 | high | unsigned char | 0x10 | - | - | - | - | 0x00: kein Fehler 0x01: Schrittverlust |
| STAT_TEMPERATUR_WARNUNG_AHL | 0/1 | high | unsigned char | 0x20 | - | - | - | - | 0x00: kein Fehler 0x01: Warnung Übertemperatur |
| STAT_TEMPERATUR_ABSCHALTUNG_AHL | 0/1 | high | unsigned char | 0x40 | - | - | - | - | 0x00: kein Fehler 0x01: Abschaltung wegen Übertemperatur |
| STAT_UNDERVOLTAGE_AHL | 0/1 | high | unsigned char | 0x80 | - | - | - | - | 0x00: kein Fehler 0x01: Unterspannung |

<a id="table-bf-led-kanal"></a>
### BF_LED_KANAL

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KANAL0 | 0/1 | low | unsigned int | 0x01 | - | - | - | - | Kanal 0 |
| KANAL1 | 0/1 | low | unsigned int | 0x02 | - | - | - | - | Kanal 1 |
| KANAL2 | 0/1 | low | unsigned int | 0x04 | - | - | - | - | Kanal 2  |

<a id="table-bf-scheinwerfer-typ"></a>
### BF_SCHEINWERFER_TYP

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHEINWERFER_HERSTELLER | 0-n | high | unsigned char | 0xE0 | SCHEINWERFER_HERSTELLER | - | - | - | Ausgabe des Scheinwerferherstellers |
| STAT_LENKERVARIANTE | 0/1 | high | unsigned char | 0x10 | - | - | - | - | 0x00: LINKSLENKER  0x01: RECHTSLENKER |
| STAT_SA_VARIANTE | 0-n | high | unsigned char | 0x0E | SCHEINWERFER_SA_VARIANTE | - | - | - | Ausgabe der SA-Variante |
| STAT_LAENDER_VARIANTE | 0-n | high | unsigned char | 0x01 | SCHEINWERFER_LAENDER_VARIANTE | - | - | - | Ausgabe der Ländervariante:  - ECE  - US |

<a id="table-bitfeld"></a>
### BITFELD

Dimensions: 18 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Kanal betroffen |
| 1 | Kanal 1 betroffen |
| 2 | Kanal 2 betroffen |
| 3 | Kanal 3 betroffen |
| 4 | Kanal 4 betroffen |
| 5 | Kanal 5 betroffen |
| 6 | Kanal 6 betroffen |
| 7 | Kanal 7 betroffen |
| 8 | Kanal 8 betroffen |
| 9 | Kanal 9 betroffen |
| 10 | Kanal 10 betroffen |
| 11 | Kanal 11 betroffen |
| 12 | Kanal 12 betroffen |
| 13 | Kanal 13 betroffen |
| 14 | Kanal 14 betroffen |
| 15 | Kanal 15 betroffen |
| 16 | Kanal 16 betroffen |
| 0xFFFF | Wert ungültig |

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

<a id="table-fahrzeug-typ"></a>
### FAHRZEUG_TYP

Dimensions: 43 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x20 | G05 |
| 0x22 | G06 |
| 0x24 | G07 |
| 0x26 | G11 |
| 0x28 | G12 |
| 0x2A | G14 |
| 0x2C | G15 |
| 0x2E | G16 |
| 0x40 | G01 |
| 0x42 | G02 |
| 0x44 | G08 |
| 0x46 | G20 |
| 0x48 | G21 |
| 0x4A | G28 |
| 0x4C | G22 |
| 0x4E | G23 |
| 0x50 | G24 |
| 0x52 | G26 |
| 0x54 | G29 |
| 0x56 | G30 |
| 0x58 | G31 |
| 0x5A | G38 |
| 0x5C | G32 |
| 0x5E | J29 |
| 0x80 | F40 |
| 0x82 | F41 |
| 0x84 | F42 |
| 0x86 | F43 |
| 0x88 | F44 |
| 0x8A | F45NF |
| 0x8C | F46NF |
| 0x8E | F54NF |
| 0x90 | F55NF |
| 0x92 | F56NF |
| 0x94 | F57NF |
| 0xC0 | I01NF |
| 0xC2 | I05 |
| 0xC4 | I12NF |
| 0x00 | RR21 |
| 0x02 | RR22 |
| 0x04 | RR24 |
| 0x06 | RR25 |
| 0xFF | Wert ungültig |

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

Dimensions: 213 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x024300 | Energiesparmode aktiv | 0 | - |
| 0x024308 | Codierung: Steuergerät ist nicht codiert | 0 | - |
| 0x024309 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 | - |
| 0x02430A | Codierung: Signatur der Codierdaten ungültig | 0 | - |
| 0x02430B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 | - |
| 0x02430C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 | - |
| 0x02430D | Codierung: Codierdaten nicht qualifiziert | 0 | - |
| 0x024324 | NVM_E_HARDWARE | 0 | - |
| 0x02FF43 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | - |
| 0x805980 | Funktion: Abblendlicht defekt | 0 | - |
| 0x805981 | Funktion: Abblendlicht Aktivierung wegen unplausibler Eingangssignale | 1 | - |
| 0x805982 | Funktion: Abblendlicht Aktivierung wegen steuergeräteinternem Eingriff FuSi | 0 | - |
| 0x805983 | Funktion: Fernlicht/Lichthupe defekt | 0 | - |
| 0x805984 | Funktion: Blendfreies Fernlicht defekt | 0 | - |
| 0x805985 | Funktion: Blendfreies Fernlicht Teilausfall | 0 | - |
| 0x805986 | Funktion: Abbiegelicht/Autobahnlicht defekt | 0 | - |
| 0x805987 | Funktion: Tagfahrlicht/Standlicht/Parklicht defekt | 0 | - |
| 0x805988 | Funktion: Fahrtrichtungsanzeiger defekt | 0 | - |
| 0x805989 | Funktion: Fahrtrichtungsanzeiger Deaktivierung wegen steuergeräteinternem Eingriff FuSi | 0 | - |
| 0x80598A | Funktion: Seitenmarkierungslicht defekt | 0 | - |
| 0x80598E | Abblendlicht: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x80598F | Abblendlicht: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x805990 | Abblendlicht: Strangunterbrechung | 0 | - |
| 0x805991 | Abblendlicht: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x805992 | Abblendlicht: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x805996 | Fernlicht: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x805997 | Fernlicht: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x805998 | Fernlicht: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x805999 | Fernlicht: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x80599A | Fernlicht: Strangunterbrechung | 0 | - |
| 0x80599D | Abbiegelicht/Autobahnlicht: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x80599E | Abbiegelicht/Autobahnlicht: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x80599F | Abbiegelicht/Autobahnlicht: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x8059A0 | Abbiegelicht/Autobahnlicht: Strangunterbrechung | 0 | - |
| 0x8059A1 | Abbiegelicht/Autobahnlicht: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x8059A4 | Tagfahrlicht/Positionslicht: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x8059A5 | Tagfahrlicht/Positionslicht: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x8059A6 | Tagfahrlicht/Positionslicht: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x8059A7 | Tagfahrlicht/Positionslicht: Strangunterbrechung | 0 | - |
| 0x8059A8 | Tagfahrlicht/Positionslicht: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x8059AB | Fahrtrichtungsanzeiger: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x8059AC | Fahrtrichtungsanzeiger: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x8059AD | Fahrtrichtungsanzeiger: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x8059AF | Fahrtrichtungsanzeiger: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x8059B0 | Fahrtrichtungsanzeiger: Strangunterbrechung | 0 | - |
| 0x8059B3 | Seitenmarkierungslicht: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x8059B4 | Seitenmarkierungslicht: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x8059B5 | Seitenmarkierungslicht: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x8059B6 | Seitenmarkierungslicht: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x8059B7 | Seitenmarkierungslicht: Strangunterbrechung | 0 | - |
| 0x8059BA | Inszenierungslicht: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x8059BB | Inszenierungslicht: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x8059BC | Inszenierungslicht: Strangunterbrechung | 0 | - |
| 0x8059BD | Inszenierungslicht: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x8059BE | Inszenierungslicht: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x8059C1 | Fernlicht Matrix: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x8059C2 | Fernlicht Matrix: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x8059C3 | Fernlicht Matrix: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x8059C4 | Fernlicht Matrix: Strangunterbrechung | 0 | - |
| 0x8059C5 | Fernlicht Matrix: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x8059C6 | Fernlicht Matrix: Segmentabschaltung fehlgeschlagen | 0 | - |
| 0x8059C9 | Fernlicht Laser: Leuchtmittel Kurzschluss nach Kl.31 | 0 | - |
| 0x8059CA | Fernlicht Laser: Leuchtmittel Kurzschluss nach UBAT | 0 | - |
| 0x8059CB | Fernlicht Laser: Leuchtmittel Strangspannung ausserhalb Toleranz | 0 | - |
| 0x8059CC | Fernlicht Laser: Strangunterbrechung | 0 | - |
| 0x8059CD | Fernlicht Laser: Leuchtmitteltreiber Übertemperaturabschaltung | 0 | - |
| 0x8059CE | Fernlicht Laser: Sicherheitsfehler Lasersystem | 0 | - |
| 0x8059CF | Fernlicht Laser: Verriegelung Lasersystem aktiv | 0 | - |
| 0x8059D1 | Binning Fehler: Abblendlicht | 0 | - |
| 0x8059D2 | Binning Fehler: Fernlicht | 0 | - |
| 0x8059D3 | Binning Fehler: Abbiegelicht/Autobahnlicht | 0 | - |
| 0x8059D4 | Binning Fehler: Tagfahrlicht/Positionslicht | 0 | - |
| 0x8059D5 | Binning Fehler: Inszenierungslicht | 0 | - |
| 0x8059D6 | Binning Fehler: Fahrtrichtungsanzeiger | 0 | - |
| 0x8059D7 | Binning Fehler: Fernlicht Matrix | 0 | - |
| 0x8059D8 | Binning Fehler: Seitenmarkierungslicht | 0 | - |
| 0x8059D9 | Binning Fehler: Fernlicht Laser | 0 | - |
| 0x8059DD | NTC Fehler: Inszenierungslicht Temperaturwert unplausibel | 0 | - |
| 0x8059DE | NTC Fehler: Fernlicht Matrix Temperaturwert unplausibel | 0 | - |
| 0x8059DF | NTC Fehler: Fahrtrichtungsanzeiger Temperaturwert unplausibel | 0 | - |
| 0x8059E0 | NTC Fehler: Fernlicht Laser Temperaturwert unplausibel | 0 | - |
| 0x8059E1 | NTC Fehler: Seitenmarkierungslicht Temperaturwert unplausibel | 0 | - |
| 0x8059E2 | NTC Fehler: Abbiegelicht/Autobahnlicht Temperaturwert unplausibel | 0 | - |
| 0x8059E3 | NTC Fehler: Abblendlicht Temperaturwert unplausibel | 0 | - |
| 0x8059E4 | NTC Fehler: Tagfahrlicht/Positionslicht Temperaturwert unplausibel | 0 | - |
| 0x8059E5 | NTC Fehler: Fernlicht Temperaturwert unplausibel | 0 | - |
| 0x8059E9 | Satellit: Kommunikationsfehler | 0 | - |
| 0x8059EA | Satellit: Unter-/Überspannung erkannt | 0 | - |
| 0x8059EB | Satellit: Parametrierung fehlgeschlagen | 0 | - |
| 0x8059EC | Satellit: Fehlender oder falscher Programmstand | 0 | - |
| 0x8059ED | Satellit: Typ passt nicht zu Codierdaten | 0 | - |
| 0x8059EE | Satellit: Kurzschluss Spannungsversorgung nach UBAT / nicht abschaltbar | 0 | - |
| 0x8059EF | Satellit: Überstrom Laserdiode | 0 | - |
| 0x8059F0 | Satellit: Kommunikationsfehler durch den Satelliten erkannt | 0 | - |
| 0x8059F1 | Lüfter: defekt | 0 | - |
| 0x8059F3 | Lüfter: Kurzschluss nach Kl.31 | 0 | - |
| 0x8059F6 | Leuchtweitenregulierung: Stellmotor Kurzschluss oder Leitungsunterbrechung an Wicklung | 0 | - |
| 0x8059F7 | Leuchtweitenregulierung: Schrittmotortreiber Übertemperaturabschaltung | 0 | - |
| 0x8059F8 | Kurvenlicht: Stellmotor Kurzschluss oder Leitungsunterbrechung an Wicklung | 0 | - |
| 0x8059F9 | Kurvenlicht: Stellmotor Referenzierung verworfen aufgrund Schrittverlust | 0 | - |
| 0x8059FA | Kurvenlicht: Stellmotor Spannungsversorgung Lagesensor gestört | 0 | - |
| 0x8059FB | Kurvenlicht: Stellmotor Sensorpegel unplausibel (Leitungsunterbrechung, Kurzschluss oder Spannungsversorgung) | 0 | - |
| 0x8059FC | Kurvenlicht: Stellmotor Referenzierung fehlgeschlagen / Sensorflanke fehlt | 0 | - |
| 0x8059FD | Kurvenlicht: Schrittmotortreiber Übertemperaturabschaltung | 0 | - |
| 0x805A01 | High Side Switch: Kurzschluss / Überstrom nach Kl.31 | 0 | - |
| 0x805A02 | High Side Switch: Open Load | 0 | - |
| 0x805A05 | Unterspannung erkannt | 1 | - |
| 0x805A06 | Überspannung erkannt | 1 | - |
| 0x805A09 | Steuergerät: interner Fehler | 0 | - |
| 0x805A0A | Steuergerät: Leuchtmitteltreiber defekt | 0 | - |
| 0x805A0B | Steuergerät: High Side Switch Kurzschlusslimit erreicht (Zählerreset erforderlich) | 0 | - |
| 0x805A0C | Steuergerät: High Side Switch Kurzschlusslimit erreicht (Steuergerätetausch erforderlich) | 0 | - |
| 0x805A0D | Steuergerät: Leuchtweitenregulierung Schrittmotortreiber defekt | 0 | - |
| 0x805A0E | Steuergerät: Kurvenlicht Schrittmotortreiber defekt | 0 | - |
| 0x805A0F | Steuergerät: Kurzschlussschalter Matrix/Tagfahrlicht defekt/nicht schaltbar | 0 | - |
| 0x805A10 | Steuergerät: L/R-Erkennung unplausibel | 0 | - |
| 0x805A11 | Satellit: interner Fehler | 0 | - |
| 0x805A12 | Satellit: Leuchtmitteltreiber defekt | 0 | - |
| 0x805A13 | Steuergerät: Plausibilisierungsfehler Codierdaten FuSi / Satellit | 0 | - |
| 0xD9C50B | B2-CAN Physikalischer Busfehler | 0 | - |
| 0xD9C514 | B2-CAN Control Module Bus OFF | 0 | - |
| 0xD9CBFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur für Testzwecke | 1 | - |
| 0xD9D400 | Botschaft 0x3C (CON_VEH) - Timeout | 1 | - |
| 0xD9D401 | Botschaft 0x3C (CON_VEH) - Fehler Alive Counter | 1 | - |
| 0xD9D402 | Botschaft 0x3C (CON_VEH) - CRC-Fehler | 1 | - |
| 0xD9D403 | Botschaft 0xCA (CTR_FN_IDC) - Fehler Alive Counter | 1 | - |
| 0xD9D404 | Botschaft 0xCA (CTR_FN_IDC) - CRC-Fehler | 1 | - |
| 0xD9D405 | Botschaft 0xCA (CTR_FN_IDC) - Timeout | 1 | - |
| 0xD9D406 | Botschaft 0x2EB (CTR_LP_EX) - Fehler Alive Counter | 1 | - |
| 0xD9D408 | Botschaft 0x2EB (CTR_LP_EX) - Timeout | 1 | - |
| 0xD9D409 | Botschaft 0x1E4 (CTR_LP_EX_2) - Timeout | 1 | - |
| 0xD9D40A | Botschaft 0x1E4 (CTR_LP_EX_2) - Fehler Alive Counter | 1 | - |
| 0xD9D40B | Botschaft 0x1E4 (CTR_LP_EX_2) - CRC-Fehler | 1 | - |
| 0xD9D40C | Botschaft 0x1A1 (V_VEH) - CRC-Fehler | 1 | - |
| 0xD9D40D | Botschaft 0x1A1 (V_VEH) - Fehler Alive Counter | 1 | - |
| 0xD9D40E | Botschaft 0x1A1 (V_VEH) - Timeout | 1 | - |
| 0xD9D40F | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Timeout | 1 | - |
| 0xD9D410 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Timeout | 1 | - |
| 0xD9D411 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Timeout | 1 | - |
| 0xD9D412 | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Timeout | 1 | - |
| 0xD9D413 | Botschaft 0xE7 (CTR_LP_EX_SPN_HRZTL) - Timeout | 1 | - |
| 0xD9D414 | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Timeout | 1 | - |
| 0xD9D517 | Botschaft 0x3C (CON_VEH) - Signal CTR_BS_PRTNT ungültig | 1 | - |
| 0xD9D518 | Botschaft 0x3C (CON_VEH) - Signal CTR_FKTN_PRTNT ungültig | 1 | - |
| 0xD9D519 | Botschaft 0x3C (CON_VEH) - Signal ST_CON_VEH ungültig | 1 | - |
| 0xD9D51A | Botschaft 0x3C (CON_VEH) - Signal QU_ST_CON_VEH ungültig | 1 | - |
| 0xD9D51B | Botschaft 0xCA (CTR_FN_IDC) - Signal CHL_CTR_FN_IDC ungültig | 1 | - |
| 0xD9D51C | Botschaft 0xCA (CTR_FN_IDC) - Signal CTR_FREQ_IDC ungültig | 1 | - |
| 0xD9D51D | Botschaft 0xCA (CTR_FN_IDC) - Signal CTR_IDC ungültig | 1 | - |
| 0xD9D51E | Botschaft 0xCA (CTR_FN_IDC) - Signal CTR_SYNC_IDC ungültig | 1 | - |
| 0xD9D521 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_BRIGLEV_LP_EX ungültig | 1 | - |
| 0xD9D522 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_FN_WELL ungültig | 1 | - |
| 0xD9D523 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_FN_GBL ungültig | 1 | - |
| 0xD9D524 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_FN_POLI ungültig | 1 | - |
| 0xD9D525 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_FN_PLI ungültig | 1 | - |
| 0xD9D526 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_FN_REMLI ungültig | 1 | - |
| 0xD9D527 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_FN_DRL ungültig | 1 | - |
| 0xD9D528 | Botschaft 0x2EB (CTR_LP_EX) - Signal CTR_FN_FMH ungültig | 1 | - |
| 0xD9D529 | Botschaft 0x1E4 (CTR_LP_EX_2) - Signal CTR_FN_DIPB_LH ungültig | 1 | - |
| 0xD9D52C | Botschaft 0x1E4 (CTR_LP_EX_2) - Signal CTR_LDSTR_LOWB_LH ungültig | 1 | - |
| 0xD9D52E | Botschaft 0x1E4 (CTR_LP_EX_2) - Signal CTR_FN_CORNL_LH ungültig | 1 | - |
| 0xD9D52F | Botschaft 0x1E4 (CTR_LP_EX_2) - Signal CTR_MOD_FN_SPFLS ungültig | 1 | - |
| 0xD9D530 | Botschaft 0x1E4 (CTR_LP_EX_2) - Signal CTR_FN_MAB ungültig | 1 | - |
| 0xD9D532 | Botschaft 0x1E4 (CTR_LP_EX_2) - Signal CTR_PHA_FN_SPFLS ungültig | 1 | - |
| 0xD9D535 | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_1_LH_XPO ungültig | 1 | - |
| 0xD9D536 | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_1_LH_YPO ungültig | 1 | - |
| 0xD9D537 | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_1_LH_WID ungültig | 1 | - |
| 0xD9D538 | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_1_LH_ID ungültig | 1 | - |
| 0xD9D539 | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_2_LH_ID ungültig | 1 | - |
| 0xD9D53A | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_2_LH_XPO ungültig | 1 | - |
| 0xD9D53B | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_2_LH_YPO ungültig | 1 | - |
| 0xD9D53C | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_2_LH_WID ungültig | 1 | - |
| 0xD9D53D | Botschaft 0x185 (CTR_LP_EX_ROI_1_LH) - Signal ROI_1_LH_SYNC_ID ungültig | 1 | - |
| 0xD9D53E | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_1_RH_ID ungültig | 1 | - |
| 0xD9D53F | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_2_RH_YPO ungültig | 1 | - |
| 0xD9D540 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_1_RH_SYNC_ID ungültig | 1 | - |
| 0xD9D541 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_1_RH_XPO ungültig | 1 | - |
| 0xD9D542 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_1_RH_YPO ungültig | 1 | - |
| 0xD9D543 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_2_RH_WID ungültig | 1 | - |
| 0xD9D544 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_1_RH_WID ungültig | 1 | - |
| 0xD9D545 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_2_RH_XPO ungültig | 1 | - |
| 0xD9D546 | Botschaft 0x187 (CTR_LP_EX_ROI_1_RH) - Signal ROI_2_RH_ID ungültig | 1 | - |
| 0xD9D547 | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_3_LH_ID ungültig | 1 | - |
| 0xD9D548 | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_4_LH_YPO ungültig | 1 | - |
| 0xD9D549 | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_2_LH_SYNC_ID ungültig | 1 | - |
| 0xD9D54A | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_3_LH_XPO ungültig | 1 | - |
| 0xD9D54B | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_3_LH_YPO ungültig | 1 | - |
| 0xD9D54C | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_4_LH_WID ungültig | 1 | - |
| 0xD9D54D | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_3_LH_WID ungültig | 1 | - |
| 0xD9D54E | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_4_LH_XPO ungültig | 1 | - |
| 0xD9D54F | Botschaft 0x186 (CTR_LP_EX_ROI_2_LH) - Signal ROI_4_LH_ID ungültig | 1 | - |
| 0xD9D550 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_4_RH_WID ungültig | 1 | - |
| 0xD9D551 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_3_RH_ID ungültig | 1 | - |
| 0xD9D552 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_4_RH_XPO ungültig | 1 | - |
| 0xD9D553 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_3_RH_YPO ungültig | 1 | - |
| 0xD9D554 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_4_RH_ID ungültig | 1 | - |
| 0xD9D555 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_3_RH_XPO ungültig | 1 | - |
| 0xD9D556 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_2_RH_SYNC_ID ungültig | 1 | - |
| 0xD9D557 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_3_RH_WID ungültig | 1 | - |
| 0xD9D558 | Botschaft 0x188 (CTR_LP_EX_ROI_2_RH) - Signal ROI_4_RH_YPO ungültig | 1 | - |
| 0xD9D559 | Botschaft 0xE7 (CTR_LP_EX_SPN_HRZTL) - Signal CTR_PO_SPN_HRZTL_LH ungültig | 1 | - |
| 0xD9D55B | Botschaft 0xE7 (CTR_LP_EX_SPN_HRZTL) - Signal CTR_V_SPN_HRZTL_LH ungültig | 1 | - |
| 0xD9D55D | Botschaft 0xE7 (CTR_LP_EX_SPN_HRZTL) - Signal CTR_SPN_ENG_HRZTL_LH ungültig | 1 | - |
| 0xD9D55F | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Signal CTR_PO_SPN_VE_LH ungültig | 1 | - |
| 0xD9D561 | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Signal CTR_V_SPN_VE_LH ungültig | 1 | - |
| 0xD9D563 | Botschaft 0xE8 (CTR_LP_EX_SPN_VE) - Signal CTR_SPN_ENG_VE_LH ungültig | 1 | - |
| 0xD9D565 | Botschaft 0x314 (STAT_FAHRLICHT) - Signal ST_LOWB ungültig | 1 | - |
| 0xD9D566 | Botschaft 0x1A1 (V_VEH) - Signal V_VEH_COG ungültig | 1 | - |
| 0xD9D567 | Botschaft 0x1A1 (V_VEH) - Signal QU_V_VEH_COG ungültig | 1 | - |
| 0xD9D568 | Botschaft 0x1A1 (V_VEH) - Signal DVCO_VEH ungültig | 1 | - |
| 0xD9D56A | Botschaft 0xCA (CTR_FN_IDC) - Signal ACV_FN_IDC ungültig | 1 | - |
| 0xD9D56B | Botschaft 0xCA (CTR_FN_IDC) - Signal OVLY_FN_IDC ungültig | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 23 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1750 | F_UW_BN | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x1751 | F_UW_TN | TEXT | High | 3 | - | 1.0 | 1.0 | 0.0 |
| 0x4000 | AUSSENTEMPARATUR | °C | High | unsigned char | - | 1.0 | 2.0 | -40.0 |
| 0x4001 | FAHRZEUGGESCHWINDIGKEIT | km/h | High | unsigned int | - | 1.0 | 64.0 | 0.0 |
| 0x4004 | SPANNUNG_LED_SENSOR | V | High | unsigned int | - | 1.0 | 20.0 | 0.0 |
| 0x4005 | SPANNUNG_KLEMME_LICHT | V | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x4006 | WIDERSTAND_BIN_NTC | kOhm | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x4007 | DREHZAHL_LUEFTER | 1/min | High | unsigned int | - | 1.0 | 2.0 | 0.0 |
| 0x400A | NR_LED_AUSGANG | HEX | High | unsigned int | - | - | - | - |
| 0x400C | TEMPERATUR_NTC | °C | High | unsigned char | - | 1.0 | 2.0 | -40.0 |
| 0x400D | NR_KURZSCHLUSSSCHALTER | HEX | High | unsigned char | - | - | - | - |
| 0x400E | NR_SATELLIT | HEX | High | unsigned char | - | - | - | - |
| 0x400F | NR_BIN_EINGANG | HEX | High | unsigned int | - | - | - | - |
| 0x4010 | NR_NTC_EINGANG | HEX | High | unsigned int | - | - | - | - |
| 0x4011 | NR_SENSOR_LASERSYSTEM | HEX | High | unsigned char | - | - | - | - |
| 0x4012 | NR_HSS_AUSGANG | HEX | High | unsigned char | - | - | - | - |
| 0x4013 | NR_WICKLUNG_SCHRITTMOTOR | HEX | High | unsigned char | - | - | - | - |
| 0x4015 | URSACHE_LUEFTERDEFEKT | HEX | High | unsigned char | - | - | - | - |
| 0x4016 | SATELLIT_FSP_ID | HEX | High | unsigned char | - | - | - | - |
| 0x4017 | SATELLIT_LSR_TEMP | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x4018 | SATELLIT_VERSORGUNG_SPANNUNG | V | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x4019 | NR_TEILSTRANG_LED_MATRIX | HEX | High | unsigned char | - | - | - | - |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-hw-model"></a>
### HW_MODEL

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | A-Muster |
| 0x40 | B-Muster |
| 0x80 | C-Muster |
| 0xC0 | D-Muster |
| 0xFF | Wert ungültig |

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

Dimensions: 42 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x430000 | Stellmotor Leuchtweitenregulierung: Referenzierung wegen Unterspannung abgebrochen | 1 | - |
| 0x430001 | Stellmotor Leuchtweitenregulierung: Verstellung wegen Unterspannung abgebrochen | 1 | - |
| 0x430002 | Stellmotor Kurvenlicht: Verstellung wegen Unterspannung abgebrochen | 1 | - |
| 0x430003 | Stellmotor Kurvenlicht: Referenzierung wegen Unterspannung abgebrochen | 1 | - |
| 0x430004 | Fahrtrichtungsanzeiger: Synchronisationsfehler | 1 | - |
| 0x43000F | Leuchtmittel: Übertemperatur 1 | 1 | - |
| 0x430010 | Leuchtmittel: Übertemperatur 2 | 1 | - |
| 0x430011 | Leuchtmittel: Übertemperatur 3 | 1 | - |
| 0x430012 | Leuchtmittel: Niedertemperatur | 1 | - |
| 0x430013 | Stellmotor: Kurzschluß nach UBat | 1 | - |
| 0x430014 | Stellmotor: Kurzschluß nach Masse | 1 | - |
| 0x430015 | Stellmotor: Leitungsunterbrechung | 1 | - |
| 0x430016 | Stellmotor: Übertemperatur Warnung | 1 | - |
| 0x430017 | Stellmotor: Tieftemperatur Warnung | 1 | - |
| 0x430018 | Steuergerät: Übertemperatur | 1 | - |
| 0x430019 | Steuergerät: Watchdog ausgelöst | 1 | - |
| 0x43001A | Steuergerät: FuSi Warnung | 1 | - |
| 0x43001B | Satellit: Fehlerspeicher intern | 0 | - |
| 0x43001E | Steuergerät: Boostwandler defekt | 0 | - |
| 0x43001F | Steuergerät: Buckwandler defekt | 0 | - |
| 0x430020 | Steuergerät: Reset Sleep Mode 11 04 | 1 | - |
| 0x430021 | Steuergerät: Reset Power Down 11 41 | 1 | - |
| 0xD9D666 | Botschaft 0x32 (ST_CENG) - Timeout | 1 | - |
| 0xD9D667 | Botschaft 0x380 (FAHRGESTELLNUMMER) - Timeout | 1 | - |
| 0xD9D668 | Botschaft 0x388 (FAHRZEUGTYP) - Timeout | 1 | - |
| 0xD9D76A | Botschaft 0x2CA (A_TEMP) - Signal TEMP_EX ungültig | 1 | - |
| 0xD9D76B | Botschaft 0x380 (FAHRGESTELLNUMMER) - Signal NO_VECH_1 ungültig | 1 | - |
| 0xD9D76C | Botschaft 0x380 (FAHRGESTELLNUMMER) - Signal NO_VECH_2 ungültig | 1 | - |
| 0xD9D76D | Botschaft 0x380 (FAHRGESTELLNUMMER) - Signal NO_VECH_3 ungültig | 1 | - |
| 0xD9D76E | Botschaft 0x380 (FAHRGESTELLNUMMER) - Signal NO_VECH_4 ungültig | 1 | - |
| 0xD9D76F | Botschaft 0x380 (FAHRGESTELLNUMMER) - Signal NO_VECH_5 ungültig | 1 | - |
| 0xD9D770 | Botschaft 0x380 (FAHRGESTELLNUMMER) - Signal NO_VECH_6 ungültig | 1 | - |
| 0xD9D771 | Botschaft 0x380 (FAHRGESTELLNUMMER) - Signal NO_VECH_7 ungültig | 1 | - |
| 0xD9D772 | Botschaft 0x388 (FAHRZEUGTYP) - Signal TYP_VEH ungültig | 1 | - |
| 0xD9D773 | Botschaft 0x388 (FAHRZEUGTYP) - Signal TYP_STE ungültig | 1 | - |
| 0xD9D774 | Botschaft 0x388 (FAHRZEUGTYP) - Signal TYP_CNT ungültig | 1 | - |
| 0xD9D775 | Botschaft 0x3A0 (FZZSTD) - Signal ST_ILK_ERRM_FZM ungültig | 1 | - |
| 0xD9D776 | Botschaft 0x330 (KILOMETERSTAND) - Signal MILE_KM ungültig | 1 | - |
| 0xD9D77F | Botschaft 0x328 (RELATIVZEIT) - Signal T_SEC_COU_REL ungültig | 1 | - |
| 0xD9D780 | Botschaft 0x32 (ST_CENG) - Signal ST_UDP ungültig | 1 | - |
| 0xD9D781 | Botschaft 0x32 (ST_CENG) - Signal ST_ENERG_SUPY ungültig | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | AUSSENTEMPARATUR | °C | High | unsigned char | - | 1.0 | 2.0 | -40.0 |
| 0x4001 | FAHRZEUGGESCHWINDIGKEIT | km/h | High | unsigned int | - | 1.0 | 64.0 | 0.0 |
| 0x4003 | NR_LED_WANDLER | HEX | High | unsigned char | - | - | - | - |
| 0x4004 | SPANNUNG_LED_SENSOR | V | High | unsigned int | - | 1.0 | 20.0 | 0.0 |
| 0x4005 | SPANNUNG_KLEMME_LICHT | V | High | unsigned char | - | 1.0 | 10.0 | 0.0 |
| 0x400A | NR_LED_AUSGANG | HEX | High | unsigned int | - | - | - | - |
| 0x400C | TEMPERATUR_NTC | °C | High | unsigned char | - | 1.0 | 2.0 | -40.0 |
| 0x400E | NR_SATELLIT | HEX | High | unsigned char | - | - | - | - |
| 0x4050 | SCHRITTMOTOR_FUNKTION | HEX | High | unsigned char | - | - | - | - |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-rdbi-ads-dop"></a>
### RDBI_ADS_DOP

Dimensions: 10 rows × 2 columns

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
| 0xff | ungültig |

<a id="table-rdbi-pc-pcs-dop"></a>
### RDBI_PC_PCS_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ECU mehrmals programmierbar |
| 0x01 | ECU mindestens einmal vollstaendig programmierbar |
| 0x02 | ECU nicht mehr programmierbar |
| 0xff | ungültig |

<a id="table-referenzierung-schrittmotor"></a>
### REFERENZIERUNG_SCHRITTMOTOR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | NICHT REFERENZIERT |
| 2 | REFERENZIERT SENSORFLANKE |
| 3 | REFERENZIERT MECHANISCHER ANSCHLAG |
| 0xFF | Wert ungültig |

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

<a id="table-res-0x4040-d"></a>
### RES_0X4040_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_VARIANT_DATA | DATA | high | data[8] | - | - | 1.0 | 1.0 | 0.0 | Bitweise Kodierung der Variante |
| STAT_CORRECT_DATA | DATA | high | data[1] | - | - | 1.0 | 1.0 | 0.0 | Gültigkeit der Variantendaten |

<a id="table-res-0x4041-d"></a>
### RES_0X4041_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HLLPOSITION_WERT | Schritte | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Position des Schrittmotors der Leuchtweitenregulierung in Anzahl Schritte |
| STAT_AHLPOSITION_WERT | Schritte | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Position des Schrittmotors des Kurvenlichts in Anzahl Schritte |

<a id="table-res-0x4042-d"></a>
### RES_0X4042_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Bit | high | BITFIELD | - | BF_FEHLERARTEN_SCHRITTMOTOR | - | - | - | liefert den Fehlerzustand des Schrittmotors der Leuchtweitenregulierung zurück |
| - | Bit | high | BITFIELD | - | BF_FEHLERARTEN_SCHRITTMOTOR_AHL | - | - | - | liefert den Fehlerzustand des Kurvenlichtmotors zurück |

<a id="table-res-0x4046-d"></a>
### RES_0X4046_D

Dimensions: 59 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_I500_TEMPERATURBEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 110°C und 120°C hatte |
| STAT_I600_TEMPERATURBEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 110°C und 120°C hatte |
| STAT_I601_TEMPERATURBEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 110°C und 120°C hatte |
| STAT_I602_TEMPERATURBEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 110°C und 120°C hatte |
| STAT_I603_TEMPERATURBEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 110°C und 120°C hatte |
| STAT_NTC_TEMPERATURBEREICH_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur zwischen 110°C und 120°C hatte  |
| STAT_I500_TEMPERATURBEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I600_TEMPERATURBEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I601_TEMPERATURBEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 120°C und 130°C hatte  |
| STAT_I602_TEMPERATURBEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I603_TEMPERATURBEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_NTC_TEMPERATURBEREICH_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der NTC eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I500_TEMPERATURBEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_I600_TEMPERATURBEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_I601_TEMPERATURBEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_I602_TEMPERATURBEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_I603_TEMPERATURBEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_NTC_TEMPERATURBEREICH_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur zwischen 130°C und 140°C hatte  |
| STAT_I500_TEMPERATURBEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I600_TEMPERATURBEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I601_TEMPERATURBEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I602_TEMPERATURBEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I603_TEMPERATURBEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_NTC_TEMPERATURBEREICH_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur zwischen 140°C und 150°C hatte  |
| STAT_I500_TEMPERATURBEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur über 150°C hatte |
| STAT_I600_TEMPERATURBEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600  eine Temperatur über 150°C hatte  |
| STAT_I601_TEMPERATURBEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur über 150°C hatte |
| STAT_I602_TEMPERATURBEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur über 150°C hatte |
| STAT_I603_TEMPERATURBEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur über 150°C hatte |
| STAT_NTC_TEMPERATURBEREICH_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur über 150°C hatte |
| STAT_BETRIEBSDAUER_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Steuergerät FLM. |
| STAT_I500_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I500_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I500 and |
| STAT_I500_MAX_TEMP_ZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I600_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I600_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I600 an |
| STAT_I600_MAX_TEMP_ZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I601_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I601_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I601 an |
| STAT_I601_MAX_TEMP_ZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I602_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I602_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I602 an |
| STAT_I602_MAX_TEMP_ZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I603_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I603_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I603 an |
| STAT_I603_MAX_TEMP_ZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_NTC_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_NTC_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von NTC an |
| STAT_NTC_MAX_TEMP_ZEIT_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I500_MAX_TEMP_GESCHW_WERT | km/h | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die Geschwindigkeit des Fahrzeugs bei der Maximaltemperatur von I500 an. |
| STAT_I500_MAX_TEMP_AUSSENTEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die Aussentemperatur zum Zeitpunkt der maximalen Temperatur von I500 an |
| STAT_I600_MAX_TEMP_GESCHW_WERT | km/h | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die Geschwindigkeit des Fahrzeugs bei der Maximaltemperatur von I600 an. |
| STAT_I600_MAX_TEMP_AUSSENTEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die Aussentemperatur zum Zeitpunkt der maximalen Temperatur von I600 an |
| STAT_I601_MAX_TEMP_GESCHW_WERT | km/h | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die Geschwindigkeit des Fahrzeugs bei der Maximaltemperatur von I601 an. |
| STAT_I601_MAX_TEMP_AUSSENTEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die Aussentemperatur zum Zeitpunkt der maximalen Temperatur von I601 an |
| STAT_I602_MAX_TEMP_GESCHW_WERT | km/h | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die Geschwindigkeit des Fahrzeugs bei der Maximaltemperatur von I602 an. |
| STAT_I602_MAX_TEMP_AUSSENTEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die Aussentemperatur zum Zeitpunkt der maximalen Temperatur von I602 an |
| STAT_I603_MAX_TEMP_GESCHW_WERT | km/h | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die Geschwindigkeit des Fahrzeugs bei der Maximaltemperatur von I603 an. |
| STAT_I603_MAX_TEMP_AUSSENTEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die Aussentemperatur zum Zeitpunkt der maximalen Temperatur von I603 an |

<a id="table-res-0x4047-d"></a>
### RES_0X4047_D

Dimensions: 48 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_I500_TEMPERATURBEREICH_2_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 100°C und 120°C hatte |
| STAT_I600_TEMPERATURBEREICH_2_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 100°C und 120°C hatte |
| STAT_I601_TEMPERATURBEREICH_2_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 100°C und 120°C hatte |
| STAT_I602_TEMPERATURBEREICH_2_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 100°C und 120°C hatte |
| STAT_I603_TEMPERATURBEREICH_2_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 100°C und 120°C hatte |
| STAT_NTC_TEMPERATURBEREICH_2_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur zwischen 100°C und 120°C hatte |
| STAT_I500_TEMPERATURBEREICH_3_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 120°C und 130°C hatte  |
| STAT_I600_TEMPERATURBEREICH_3_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I601_TEMPERATURBEREICH_3_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I602_TEMPERATURBEREICH_3_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I603_TEMPERATURBEREICH_3_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 120°C und 130°C hatte  |
| STAT_NTC_TEMPERATURBEREICH_3_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der NTC eine Temperatur zwischen 120°C und 130°C hatte |
| STAT_I500_TEMPERATURBEREICH_4_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_I600_TEMPERATURBEREICH_4_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 130°C und 140°C hatte  |
| STAT_I601_TEMPERATURBEREICH_4_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_I602_TEMPERATURBEREICH_4_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_I603_TEMPERATURBEREICH_4_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 130°C und 140°C hatte |
| STAT_NTC_TEMPERATURBEREICH_4_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur zwischen 130°C und 140°C hatte  |
| STAT_I500_TEMPERATURBEREICH_5_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I600_TEMPERATURBEREICH_5_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I601_TEMPERATURBEREICH_5_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I602_TEMPERATURBEREICH_5_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_I603_TEMPERATURBEREICH_5_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur zwischen 140°C und 150°C hatte |
| STAT_NTC_TEMPERATURBEREICH_5_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur zwischen 140°C und 150°C hatte  |
| STAT_I500_TEMPERATURBEREICH_6_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I500 eine Temperatur über 150°C hatte |
| STAT_I600_TEMPERATURBEREICH_6_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I600  eine Temperatur über 150°C hatte  |
| STAT_I601_TEMPERATURBEREICH_6_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I601 eine Temperatur über 150°C hatte |
| STAT_I602_TEMPERATURBEREICH_6_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I602 eine Temperatur über 150°C hatte |
| STAT_I603_TEMPERATURBEREICH_6_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der I603 eine Temperatur über 150°C hatte  |
| STAT_NTC_TEMPERATURBEREICH_6_WERT | min | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zeit in der der int. NTC eine Temperatur über 150°C hatte  |
| STAT_I500_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I500_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I500 and |
| STAT_I500_MAX_TEMP_ZEIT_WERT | s | high | signed long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I600_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I600_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I600 an |
| STAT_I600_MAX_TEMP_ZEIT_WERT | s | high | signed long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I601_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I601_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I601 an |
| STAT_I601_MAX_TEMP_ZEIT_WERT | s | high | signed long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I602_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I602_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I602 an |
| STAT_I602_MAX_TEMP_ZEIT_WERT | s | high | signed long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_I603_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_I603_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von I603 an |
| STAT_I603_MAX_TEMP_ZEIT_WERT | s | high | signed long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |
| STAT_NTC_MAX_KONFIG_WERT | HEX | high | signed int | - | - | - | - | - | Gibt an welche Kanäle bei max. Temperatur eingeschaltet waren. Bitkodierte Kanalangabe |
| STAT_NTC_MAX_TEMP_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Gibt die maximale Temperatur von NTC an |
| STAT_NTC_MAX_TEMP_ZEIT_WERT | s | high | signed long | - | - | 1.0 | 1.0 | 0.0 | Gibt den Zeitpunkt der maximalen Temperatur an |

<a id="table-res-0x4048-d"></a>
### RES_0X4048_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMPERATUR_I500_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aktuelle Temperatur I500 |
| STAT_TEMPERATUR_I600_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aktuelle Temperatur I600 |
| STAT_TEMPERATUR_I601_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aktuelle Temperatur I601 |
| STAT_TEMPERATUR_I602_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aktuelle Temperatur I602 |
| STAT_TEMPERATUR_I603_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aktuelle Temperatur I603 |
| STAT_TEMPERATUR_NTC_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | Aktuelle Temperatur NTC-FLM2 |

<a id="table-res-0x4049-d"></a>
### RES_0X4049_D

Dimensions: 18 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SI_SENSOR_1_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_2_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_3_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_4_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_5_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_6_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_7_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_8_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_9_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_10_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_11_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_12_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_13_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_14_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_R_L_DETECTION_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_LUEFTER_1_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_LUEFTER_2_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |
| STAT_SI_SENSOR_AHL_HW_WERT | V | high | unsigned int | - | - | 5.0 | 1023.0 | 0.0 | Eingangspannung am Analogeingang |

<a id="table-res-0x404b-d"></a>
### RES_0X404B_D

Dimensions: 11 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_R0_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R1_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R2_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R3_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R4_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R5_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R6_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R7_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R8_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_R9_WERT | mOhm | high | signed int | - | - | 1.0 | 1.0 | 0.0 | gibt den Widerstandswert des im Namen genannten Shunts zurück |
| STAT_VALID | 0/1 | high | signed char | - | - | - | - | - | gibt an, ob die konfigurierte Widerstandswerte gültig sind oder Defaultwerte verwendet werden |

<a id="table-res-0x404d-d"></a>
### RES_0X404D_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SSM_FLAG_WERT | HEX | high | unsigned int | - | - | - | - | - | SSM_FLAG |
| STAT_EXTRAINFO_WERT | HEX | high | unsigned long | - | - | - | - | - | extra info |
| STAT_TIMESTAMP_WERT | HEX | high | unsigned long | - | - | - | - | - | Zeitstempel |

<a id="table-res-0x4051-d"></a>
### RES_0X4051_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KALIBRIERUNG_DATA | DATA | high | data[80] | - | - | 1.0 | 1.0 | 0.0 | Werte Kalibrierung der LED-Treiber |
| STAT_GUELTIGKEIT | 0/1 | high | unsigned char | - | - | - | - | - | 0x00: Kalibrierdaten gültig 0x01: Kalibrierdaten ungültig |

<a id="table-res-0xa549-r"></a>
### RES_0XA549_R

Dimensions: 34 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTEST_KANAL_1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_3_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_4_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_5_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_6_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_7_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_8_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_9_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_10_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_11_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_12_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_13_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_14_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KANAL_15_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LR_ERKENNUNG_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_TEMPERATURSENSOREN_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LED_BINNING_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LUEFTER_1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_LUEFTER_2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_HIGHSIDE_SWITCH_1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_HIGHSIDE_SWITCH_2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_STELLMOTOR_LWR_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_STELLMOTOR_AHL_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_3_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_4_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_5_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_6_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_7_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_8_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_9_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |
| STAT_FUNKTIONSTEST_KURZSCHLUSSSCHALTER_10_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |

<a id="table-res-0xa54a-r"></a>
### RES_0XA54A_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FUNKTIONSTEST_LASER_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ergebnis Systemtest: 0...mit Fehler beendet 1...ohne Fehler beendet 2...noch nicht beendet |

<a id="table-res-0xa54c-r"></a>
### RES_0XA54C_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SATELLIT_DATA | + | - | - | DATA | high | data[252] | - | - | 1.0 | 1.0 | 0.0 | Ergebnis der Diagnoseanfrage Satelliten-Elektronik |

<a id="table-res-0xa54d-r"></a>
### RES_0XA54D_R

Dimensions: 48 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LUEFTERBEWEGUNG | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0: Lüfter nicht aktiv 1: Lüfter aktiv |
| STAT_PRUEFUNGSFORTSCHRITT_WERT | - | - | + | HEX | high | unsigned char | - | - | - | - | - | 0: Lüfter nicht aktiv  1: Prüfung läuft  2: Prüfung abgeschlossen |
| STAT_PRUEFERGEBNIS_WERT | - | - | + | HEX | high | unsigned char | - | - | - | - | - | 0: kein Ergebnis  1: ohne Fehler abgeschlossen  2: mit Fehlern abgeschlossen |
| STAT_URSACHE_FEHLERERKENNUNG_WERT | - | - | + | HEX | high | unsigned char | - | - | - | - | - | 0: kein Fehler erkannt  1: Gradient n.i.O.  2: Gradient n.i.O und Thermo3  3: Thermo3 |
| STAT_ZAEHLER_ENTPRELLUNG_LED1_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED2_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED3_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED4_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED5_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED6_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED7_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED8_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED9_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED10_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED12_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED13_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED14_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_ZAEHLER_ENTPRELLUNG_LED15_WERT | - | - | + | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Zählerstand Entprellung LED-Ausgang |
| STAT_GRADIENT_LED1_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED2_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED3_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED4_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED5_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED6_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED7_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED8_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED9_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED10_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED11_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED12_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED13_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED14_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRADIENT_LED15_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Temperaturgradient des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED1_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED2_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED3_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED4_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED5_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED6_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED7_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED8_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED9_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED10_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED11_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED12_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED13_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED14_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |
| STAT_GRENZWERT_GRADIENT_LED15_WERT | - | - | + | K/ms | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Grenzwert für den Temperaturgradienten des jeweiligen LED-Ausgangs |

<a id="table-res-0xa54e-r"></a>
### RES_0XA54E_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_POSITION_AHL_WERT | - | - | + | ° | high | unsigned int | - | - | 1.0 | 100.0 | -20.0 | Ausgabe der Position des Schrittmotors AHL |

<a id="table-res-0xa54f-r"></a>
### RES_0XA54F_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_POSITION_LWR_WERT | - | - | + | ° | high | unsigned int | - | - | 1.0 | 100.0 | -20.0 | Ausgabe der Position des Schrittmotors LWR |

<a id="table-res-0xaff3-r"></a>
### RES_0XAFF3_R

Dimensions: 10 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PWM_KSS_1_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_2_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_3_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_4_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_5_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_6_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_7_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_8_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_9_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |
| STAT_PWM_KSS_10_WERT | - | - | + | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Gibt die PWM des jeweiligen Kurzschlussschalters aus. |

<a id="table-res-0xd6d3-d"></a>
### RES_0XD6D3_D

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHRITTVERLUSTE_BEREICH_1_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 1. |
| STAT_SCHRITTVERLUSTE_BEREICH_2_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 2. |
| STAT_SCHRITTVERLUSTE_BEREICH_3_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 3. |
| STAT_SCHRITTVERLUSTE_BEREICH_4_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 4. |
| STAT_SCHRITTVERLUSTE_BEREICH_5_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 5. |
| STAT_SCHRITTVERLUSTE_BEREICH_6_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Schrittverluste im Bereich 6. |
| STAT_SCHRITTVERLUSTE_KUMMLIERT_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Summe aller bisheriger Schrittverluste seit letztem Zählerreset. |

<a id="table-res-0xd6db-d"></a>
### RES_0XD6DB_D

Dimensions: 60 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PWM_KANAL_1_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 1 |
| STAT_STRANGSTROM_KANAL_1_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 1 |
| STAT_STRANGSPANNUNG_KANAL_1_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 1 |
| STAT_STRANGSPANNUNG_KANAL_1_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 1 |
| STAT_PWM_KANAL_2_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 2 |
| STAT_STRANGSTROM_KANAL_2_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 2 |
| STAT_STRANGSPANNUNG_KANAL_2_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 2 |
| STAT_STRANGSPANNUNG_KANAL_2_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 2 |
| STAT_PWM_KANAL_3_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 3 |
| STAT_STRANGSTROM_KANAL_3_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 3 |
| STAT_STRANGSPANNUNG_KANAL_3_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 3 |
| STAT_STRANGSPANNUNG_KANAL_3_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 3 |
| STAT_PWM_KANAL_4_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 4 |
| STAT_STRANGSTROM_KANAL_4_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 4 |
| STAT_STRANGSPANNUNG_KANAL_4_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 4 |
| STAT_STRANGSPANNUNG_KANAL_4_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 4 |
| STAT_PWM_KANAL_5_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 5 |
| STAT_STRANGSTROM_KANAL_5_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 5 |
| STAT_STRANGSPANNUNG_KANAL_5_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 5 |
| STAT_STRANGSPANNUNG_KANAL_5_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 5 |
| STAT_PWM_KANAL_6_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 6 |
| STAT_STRANGSTROM_KANAL_6_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 6 |
| STAT_STRANGSPANNUNG_KANAL_6_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 6 |
| STAT_STRANGSPANNUNG_KANAL_6_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 6 |
| STAT_PWM_KANAL_7_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 7 |
| STAT_STRANGSTROM_KANAL_7_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 7 |
| STAT_STRANGSPANNUNG_KANAL_7_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 7 |
| STAT_STRANGSPANNUNG_KANAL_7_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 7 |
| STAT_PWM_KANAL_8_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 8 |
| STAT_STRANGSTROM_KANAL_8_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 8 |
| STAT_STRANGSPANNUNG_KANAL_8_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 8 |
| STAT_STRANGSPANNUNG_KANAL_8_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 8 |
| STAT_PWM_KANAL_9_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 9 |
| STAT_STRANGSTROM_KANAL_9_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 9 |
| STAT_STRANGSPANNUNG_KANAL_9_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 9 |
| STAT_STRANGSPANNUNG_KANAL_9_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 9 |
| STAT_PWM_KANAL_10_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 10 |
| STAT_STRANGSTROM_KANAL_10_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 10 |
| STAT_STRANGSPANNUNG_KANAL_10_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 10 |
| STAT_STRANGSPANNUNG_KANAL_10_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 10 |
| STAT_PWM_KANAL_11_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 11 |
| STAT_STRANGSTROM_KANAL_11_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 11 |
| STAT_STRANGSPANNUNG_KANAL_11_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 11 |
| STAT_STRANGSPANNUNG_KANAL_11_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 11 |
| STAT_PWM_KANAL_12_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 12 |
| STAT_STRANGSTROM_KANAL_12_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 12 |
| STAT_STRANGSPANNUNG_KANAL_12_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 12 |
| STAT_STRANGSPANNUNG_KANAL_12_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 12 |
| STAT_PWM_KANAL_13_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 13 |
| STAT_STRANGSTROM_KANAL_13_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 13 |
| STAT_STRANGSPANNUNG_KANAL_13_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 13 |
| STAT_STRANGSPANNUNG_KANAL_13_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 13 |
| STAT_PWM_KANAL_14_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 14 |
| STAT_STRANGSTROM_KANAL_14_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 14 |
| STAT_STRANGSPANNUNG_KANAL_14_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 14 |
| STAT_STRANGSPANNUNG_KANAL_14_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 14 |
| STAT_PWM_KANAL_15_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Kanal 15 |
| STAT_STRANGSTROM_KANAL_15_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom Kanal 15 |
| STAT_STRANGSPANNUNG_KANAL_15_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Strangspannung Kanal 15 |
| STAT_STRANGSPANNUNG_KANAL_15_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Strangspannung on/off-Phase Kanal 15 |

<a id="table-res-0xd6df-d"></a>
### RES_0XD6DF_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PWM_AUSGANG_1_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Ausgang 1 |
| STAT_STROM_AUSGANG_1_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strom Wert Ausgang 1 |
| STAT_SPANNUNG_AUSGANG_1_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannung Wert Ausgang 1 |
| STAT_SPANNUNG_AUSGANG_1_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Phase Ausgang 1:  0: off-Phase 1: on-Phase |
| STAT_PWM_AUSGANG_2_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Ausgang 2 |
| STAT_STROM_AUSGANG_2_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strom Wert Ausgang 2 |
| STAT_SPANNUNG_AUSGANG_2_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannung Wert Ausgang 2 |
| STAT_SPANNUNG_AUSGANG_2_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Phase Ausgang 2:  0: off-Phase 1: on-Phase |
| STAT_PWM_AUSGANG_3_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert Ausgang 3 |
| STAT_STROM_AUSGANG_3_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strom Wert Ausgang 3 |
| STAT_SPANNUNG_AUSGANG_3_WERT | V | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Spannung Wert Ausgang 3 |
| STAT_SPANNUNG_AUSGANG_3_PHASE | 0/1 | high | unsigned char | - | - | - | - | - | Phase Ausgang 3:  0: off-Phase 1: on-Phase |

<a id="table-res-0xd7a7-d"></a>
### RES_0XD7A7_D

Dimensions: 48 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ST_FE_1_LH_FN_IDC_WERT | HEX | - | unsigned char | - | - | - | - | - | Blinken links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_FMH_WERT | HEX | - | unsigned char | - | - | - | - | - | Heimleuchten links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_REMLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Remote-Light links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_SPFLS_WERT | HEX | - | unsigned char | - | - | - | - | - | Sonderblinken links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_DRL_WERT | HEX | - | unsigned char | - | - | - | - | - | Tagfahrlicht links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_LDSTR_LOWB_WERT | HEX | - | unsigned char | - | - | - | - | - | Lichtverteilung Fahrlicht links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_DIPB_WERT | HEX | - | unsigned char | - | - | - | - | - | Abblendlicht links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_PLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Parklicht links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_POLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Standlicht links vorne. [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_MAB_WERT | HEX | - | unsigned char | - | - | - | - | - | Fernlicht links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_FN_WELL_WERT | HEX | - | unsigned char | - | - | - | - | - | Begrüßungslicht links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_LH_BRIGLEV_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Helligkeit Leuchten links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ALIV_FE_1_LH_ST_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Alivezähler FLM links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_CORNL_WERT | HEX | - | unsigned char | - | - | - | - | - | Abbiegelicht links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_FMH_WERT | HEX | - | unsigned char | - | - | - | - | - | Heimleuchten links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_REMLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Remote-Light links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_SPFLS_WERT | HEX | - | unsigned char | - | - | - | - | - | Sonderblinken links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_DRL_WERT | HEX | - | unsigned char | - | - | - | - | - | Tagfahrlicht links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_LDSTR_LOWB_WERT | HEX | - | unsigned char | - | - | - | - | - | Lichtverteilung Fahrlicht links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_DIPB_WERT | HEX | - | unsigned char | - | - | - | - | - | Abblendlicht links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_MAB_WERT | HEX | - | unsigned char | - | - | - | - | - | Fernlicht links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_FN_WELL_WERT | HEX | - | unsigned char | - | - | - | - | - | Begrüßungslicht links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_LH_BRIGLEV_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Helligkeit Leuchten links vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ALIV_FE_2_LH_ST_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Alivezähler FLM links.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_IDC_WERT | HEX | - | unsigned char | - | - | - | - | - | Blinken rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_FMH_WERT | HEX | - | unsigned char | - | - | - | - | - | Heimleuchten rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_REMLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Remote-Light rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_SPFLS_WERT | HEX | - | unsigned char | - | - | - | - | - | Sonderblinken rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_DRL_WERT | HEX | - | unsigned char | - | - | - | - | - | Tagfahrlicht rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_LDSTR_LOWB_WERT | HEX | - | unsigned char | - | - | - | - | - | Lichtverteilung Fahrlicht rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_DIPB_WERT | HEX | - | unsigned char | - | - | - | - | - | Abblendlicht rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_PLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Parklicht rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_POLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Standlicht rechts vorne. [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_MAB_WERT | HEX | - | unsigned char | - | - | - | - | - | Fernlicht rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_FN_WELL_WERT | HEX | - | unsigned char | - | - | - | - | - | Begrüßungslicht rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_1_RH_BRIGLEV_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Helligkeit Leuchten rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ALIV_FE_1_RH_ST_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Alivezähler FLM rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_CORNL_WERT | HEX | - | unsigned char | - | - | - | - | - | Abbiegelicht rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_FMH_WERT | HEX | - | unsigned char | - | - | - | - | - | Heimleuchten rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_REMLI_WERT | HEX | - | unsigned char | - | - | - | - | - | Remote-Light rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_SPFLS_WERT | HEX | - | unsigned char | - | - | - | - | - | Sonderblinken rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_DRL_WERT | HEX | - | unsigned char | - | - | - | - | - | Tagfahrlicht rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_LDSTR_LOWB_WERT | HEX | - | unsigned char | - | - | - | - | - | Lichtverteilung Fahrlicht rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_DIPB_WERT | HEX | - | unsigned char | - | - | - | - | - | Abblendlicht rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_MAB_WERT | HEX | - | unsigned char | - | - | - | - | - | Fernlicht rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_FN_WELL_WERT | HEX | - | unsigned char | - | - | - | - | - | Begrüßungslicht rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ST_FE_2_RH_BRIGLEV_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Helligkeit Leuchten rechts vorne.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |
| STAT_ALIV_FE_2_RH_ST_LP_EX_WERT | HEX | - | unsigned char | - | - | - | - | - | Alivezähler FLM rechts.  [HEX] in BIN für Statusinhalt gemäß aktuell gültiger NK B2-CAN. |

<a id="table-res-0xd7ad-d"></a>
### RES_0XD7AD_D

Dimensions: 38 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 1. |
| STAT_LED_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 2. |
| STAT_LED_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 3. |
| STAT_LED_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 4. |
| STAT_LED_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 5. |
| STAT_LED_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 6. |
| STAT_LED_7_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 7. |
| STAT_LED_8_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 8. |
| STAT_LED_9_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 9. |
| STAT_LED_10_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 10. |
| STAT_LED_11_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 11. |
| STAT_LED_12_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 12. |
| STAT_LED_13_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 13. |
| STAT_LED_14_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 14. |
| STAT_LED_15_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer LED-Ausgang 15. |
| STAT_HSS_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Highside-Switch 1 (SAT/LAMPE). |
| STAT_HSS_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Highside-Switch 2 (SAT/LAMPE). |
| STAT_HSS_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Highside-Switch 3 (LÜFTER). |
| STAT_KSS_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 1. |
| STAT_KSS_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 2. |
| STAT_KSS_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 3. |
| STAT_KSS_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 4. |
| STAT_KSS_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 5. |
| STAT_KSS_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 6. |
| STAT_KSS_7_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 7. |
| STAT_KSS_8_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 8. |
| STAT_KSS_9_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 9. |
| STAT_KSS_10_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Kurzschlussschalter 10. |
| STAT_AHL_HALTESTROM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Haltestrom AHL Schrittmotor. |
| STAT_AHL_VERSTELLSTROM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Verstellstrom AHL Schrittmotor. |
| STAT_AHL_VERSTELLUNGEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Verstellungen AHL Schrittmotor. |
| STAT_LWR_HALTESTROM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Haltestrom LWR Schrittmotor. |
| STAT_LWR_VERSTELLSTROM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Verstellstrom LWR Schrittmotor. |
| STAT_LWR_VERSTELLUNGEN_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Verstellungen LWR Schrittmotor. |
| STAT_SATELLIT_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Satellit 1. |
| STAT_SATELLIT_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Satellit 2. |
| STAT_SATELLIT_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Satellit 3. |
| STAT_FLM_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Betriebsdauer Steuergerät FLM. |

<a id="table-res-0xd7ba-d"></a>
### RES_0XD7BA_D

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RESET_SWRESET_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch die Software. |
| STAT_RESET_WATCHDOG_0_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch internen Watchdog 1. |
| STAT_RESET_WATCHDOG_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch internen Watchdog 2. |
| STAT_RESET_CLOCKMONITOR_0_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch den internen Oszillator (Clock Monitor 0). |
| STAT_RESET_CLOCKMONITOR_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch den Hauptoszillator (Clock Monitor 1). |
| STAT_RESET_CLOCKMONITOR_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch den PLL (Clock Monitor 2). |
| STAT_RESET_LOW_VOLTAGE_I_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch Spannung: LVI - Spannungsversorgung der ECU zu gering. |
| STAT_RESET_CORE_VOLTAGE_M_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch Spannung: CVM - Core Spannung zu gering. |
| STAT_RESET_EXTERNAL_RESET_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch externen Watchdog. |
| STAT_RESET_POWER_ON_RESET_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch Power On. |
| STAT_RESET_ISO_RESET_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets in ISO Area. |
| STAT_RESET_UNDEFINED_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch undefinierte Ursachen. |
| STAT_RESET_UNKNOWN_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch unbekannte Ursachen. |
| STAT_RESET_MULTIPLE_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Anzahl der Resets durch mehrere Resetquellen gleichzeitig. |

<a id="table-res-0xd7bc-d"></a>
### RES_0XD7BC_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZLAUF_BEGONNEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der begonnenen Referenzläufe des AHL Schrittmotors. |
| STAT_REFERENZLAUF_ABGESCHLOSSEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der abgeschlossenen Referenzläufe des AHL Schrittmotors. |

<a id="table-res-0xd7be-d"></a>
### RES_0XD7BE_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZLAUF_BEGONNEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der begonnenen Referenzläufe des LWR Schrittmotors. |
| STAT_REFERENZLAUF_ABGESCHLOSSEN_WERT | - | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Anzahl der abgeschlossenen Referenzläufe des LWR Schrittmotors. |

<a id="table-res-0xd9bd-d"></a>
### RES_0XD9BD_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STRANGSTROM_WERT | mA | high | unsigned int | - | - | 1.0 | 1.0 | 0.0 | Strangstrom des LED-Ausgangs für Blinker. |
| STAT_PWM_WERT | % | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | PWM Wert des LED-Ausgangs für Blinker. |

<a id="table-res-0xd9bf-d"></a>
### RES_0XD9BF_D

Dimensions: 96 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FLM_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC FLM in Temperaturklasse 1 |
| STAT_FLM_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC FLM in Temperaturklasse 2 |
| STAT_FLM_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC FLM in Temperaturklasse 3 |
| STAT_FLM_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC FLM in Temperaturklasse 4 |
| STAT_FLM_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC FLM in Temperaturklasse 5 |
| STAT_FLM_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC FLM in Temperaturklasse 6 |
| STAT_LM_1_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 1 in Temperaturklasse 1 |
| STAT_LM_1_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 1 in Temperaturklasse 2 |
| STAT_LM_1_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 1 in Temperaturklasse 3 |
| STAT_LM_1_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 1 in Temperaturklasse 4 |
| STAT_LM_1_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 1 in Temperaturklasse 5 |
| STAT_LM_1_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 1 in Temperaturklasse 6 |
| STAT_LM_2_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 2 in Temperaturklasse 1 |
| STAT_LM_2_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 2 in Temperaturklasse 2 |
| STAT_LM_2_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 2 in Temperaturklasse 3 |
| STAT_LM_2_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 2 in Temperaturklasse 4 |
| STAT_LM_2_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 2 in Temperaturklasse 5 |
| STAT_LM_2_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 2 in Temperaturklasse 6 |
| STAT_LM_3_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 3 in Temperaturklasse 1 |
| STAT_LM_3_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 3 in Temperaturklasse 2 |
| STAT_LM_3_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 3 in Temperaturklasse 3 |
| STAT_LM_3_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 3 in Temperaturklasse 4 |
| STAT_LM_3_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 3 in Temperaturklasse 5 |
| STAT_LM_3_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 3 in Temperaturklasse 6 |
| STAT_LM_4_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 4 in Temperaturklasse 1 |
| STAT_LM_4_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 4 in Temperaturklasse 2 |
| STAT_LM_4_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 4 in Temperaturklasse 3 |
| STAT_LM_4_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 4 in Temperaturklasse 4 |
| STAT_LM_4_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 4 in Temperaturklasse 5 |
| STAT_LM_4_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 4 in Temperaturklasse 6 |
| STAT_LM_5_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 5 in Temperaturklasse 1 |
| STAT_LM_5_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 5 in Temperaturklasse 2 |
| STAT_LM_5_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 5 in Temperaturklasse 3 |
| STAT_LM_5_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 5 in Temperaturklasse 4 |
| STAT_LM_5_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 5 in Temperaturklasse 5 |
| STAT_LM_5_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 5 in Temperaturklasse 6 |
| STAT_LM_6_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 6 in Temperaturklasse 1 |
| STAT_LM_6_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 6 in Temperaturklasse 2 |
| STAT_LM_6_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 6 in Temperaturklasse 3 |
| STAT_LM_6_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 6 in Temperaturklasse 4 |
| STAT_LM_6_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 6 in Temperaturklasse 5 |
| STAT_LM_6_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 6 in Temperaturklasse 6 |
| STAT_LM_7_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 7 in Temperaturklasse 1 |
| STAT_LM_7_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 7 in Temperaturklasse 2 |
| STAT_LM_7_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 7 in Temperaturklasse 3 |
| STAT_LM_7_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 7 in Temperaturklasse 4 |
| STAT_LM_7_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 7 in Temperaturklasse 5 |
| STAT_LM_7_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 7 in Temperaturklasse 6 |
| STAT_LM_8_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 8 in Temperaturklasse 1 |
| STAT_LM_8_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 8 in Temperaturklasse 2 |
| STAT_LM_8_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 8 in Temperaturklasse 3 |
| STAT_LM_8_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 8 in Temperaturklasse 4 |
| STAT_LM_8_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 8 in Temperaturklasse 5 |
| STAT_LM_8_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 8 in Temperaturklasse 6 |
| STAT_LM_9_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 9 in Temperaturklasse 1 |
| STAT_LM_9_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 9 in Temperaturklasse 2 |
| STAT_LM_9_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 9 in Temperaturklasse 3 |
| STAT_LM_9_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 9 in Temperaturklasse 4 |
| STAT_LM_9_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 9 in Temperaturklasse 5 |
| STAT_LM_9_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 9 in Temperaturklasse 6 |
| STAT_LM_10_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 10 in Temperaturklasse 1 |
| STAT_LM_10_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 10 in Temperaturklasse 2 |
| STAT_LM_10_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 10 in Temperaturklasse 3 |
| STAT_LM_10_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 10 in Temperaturklasse 4 |
| STAT_LM_10_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 10 in Temperaturklasse 5 |
| STAT_LM_10_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 10 in Temperaturklasse 6 |
| STAT_LM_11_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 11 in Temperaturklasse 1 |
| STAT_LM_11_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 11 in Temperaturklasse 2 |
| STAT_LM_11_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 11 in Temperaturklasse 3 |
| STAT_LM_11_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 11 in Temperaturklasse 4 |
| STAT_LM_11_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 11 in Temperaturklasse 5 |
| STAT_LM_11_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 11 in Temperaturklasse 6 |
| STAT_LM_12_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 12 in Temperaturklasse 1 |
| STAT_LM_12_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 12 in Temperaturklasse 2 |
| STAT_LM_12_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 12 in Temperaturklasse 3 |
| STAT_LM_12_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 12 in Temperaturklasse 4 |
| STAT_LM_12_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 12 in Temperaturklasse 5 |
| STAT_LM_12_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 12 in Temperaturklasse 6 |
| STAT_LM_13_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 13 in Temperaturklasse 1 |
| STAT_LM_13_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 13 in Temperaturklasse 2 |
| STAT_LM_13_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 13 in Temperaturklasse 3 |
| STAT_LM_13_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 13 in Temperaturklasse 4 |
| STAT_LM_13_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 13 in Temperaturklasse 5 |
| STAT_LM_13_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 13 in Temperaturklasse 6 |
| STAT_LM_14_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 14 in Temperaturklasse 1 |
| STAT_LM_14_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 14 in Temperaturklasse 2 |
| STAT_LM_14_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 14 in Temperaturklasse 3 |
| STAT_LM_14_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 14 in Temperaturklasse 4 |
| STAT_LM_14_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 14 in Temperaturklasse 5 |
| STAT_LM_14_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 14 in Temperaturklasse 6 |
| STAT_LM_15_TEMPKLASSE_1_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 15 in Temperaturklasse 1 |
| STAT_LM_15_TEMPKLASSE_2_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 15 in Temperaturklasse 2 |
| STAT_LM_15_TEMPKLASSE_3_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 15 in Temperaturklasse 3 |
| STAT_LM_15_TEMPKLASSE_4_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 15 in Temperaturklasse 4 |
| STAT_LM_15_TEMPKLASSE_5_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 15 in Temperaturklasse 5 |
| STAT_LM_15_TEMPKLASSE_6_WERT | s | high | unsigned long | - | - | 1.0 | 1.0 | 0.0 | Sensor NTC Leuchtmittel 15 in Temperaturklasse 6 |

<a id="table-res-0xd9c8-d"></a>
### RES_0XD9C8_D

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CRC_WERT | HEX | high | unsigned char | - | - | - | - | - | Inhalt CRC-Signal  [0x00...0xFF] |
| STAT_ALIVE_WERT | HEX | high | unsigned char | - | - | - | - | - | Inhalt Alive-Signal  [0x0...0xF] |
| STAT_SEC_1_WERT | HEX | high | unsigned char | - | - | - | - | - | Sicherheitsstatus Sensor 1 |
| STAT_SEC_2_WERT | HEX | high | unsigned char | - | - | - | - | - | Sicherheitsstatus Sensor 2 |
| STAT_U_LSR_WERT | HEX | high | unsigned int | - | - | - | - | - | Rohwert Spannung Laser  [0x000...0x3FF]  0...51,15V in 50mV-Schritten |
| STAT_I_LSR_WERT | HEX | high | unsigned int | - | - | - | - | - | Rohwert Strom Laser  [0x000...0x3FF]  0-5,115A in 5mA-Schritten |
| STAT_T_LSR_WERT | HEX | high | unsigned char | - | - | - | - | - | Rohwert Temperatur Laser  [0x00...0xFC]  -40 bis +212 °C in 1K-Schritten (Offset: -40K) |
| STAT_PWM_LSR_WERT | HEX | high | unsigned char | - | - | - | - | - | Rohwert PWM Laser  [0x00...0xC8]  0-100% in 0,5%-Schritten |
| STAT_DRV_LSR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status Lasertreiber  0: kein Fehler  1: Fehler (KS/Leerlauf) |
| STAT_BIN_LSR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status Binning Laser  0: kein Fehler  1: Fehler (KS/Leerlauf) |
| STAT_NTC_LSR_WERT | HEX | high | unsigned char | - | - | - | - | - | Status NTC Laser  0: kein Fehler  1: Fehler (KS/Leerlauf) |
| STAT_LM_LSR_WERT | HEX | high | unsigned char | - | - | - | - | - | Leuchtmittelstatus Laser  0: LM nicht aktiv  1: LM aktiv |

<a id="table-res-0xd9f6-d"></a>
### RES_0XD9F6_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIEFTEMPERATURMODUS | 0/1 | high | unsigned char | - | - | - | - | - | Temperaturmodus: 1: aktiv  0: nicht aktiv |
| STAT_NORMALMODUS | 0/1 | high | unsigned char | - | - | - | - | - | Temperaturmodus: 1: aktiv  0: nicht aktiv |
| STAT_HOCHTEMPERATURMODUS | 0/1 | high | unsigned char | - | - | - | - | - | Temperaturmodus: 1: aktiv  0: nicht aktiv |

<a id="table-res-0xd9f7-d"></a>
### RES_0XD9F7_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TIEFTEMPERATURMODUS | 0/1 | high | unsigned char | - | - | - | - | - | Temperaturmodus: 1: aktiv  0: nicht aktiv |
| STAT_NORMALMODUS | 0/1 | high | unsigned char | - | - | - | - | - | Temperaturmodus: 1: aktiv  0: nicht aktiv |
| STAT_HOCHTEMPERATURMODUS | 0/1 | high | unsigned char | - | - | - | - | - | Temperaturmodus: 1: aktiv  0: nicht aktiv |

<a id="table-res-0xd9f8-d"></a>
### RES_0XD9F8_D

Dimensions: 45 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BINNINGKLASSE_LED_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang |
| STAT_BINNINGKLASSE_LED_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_4_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_5_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNIN_GKLASSE_LED_6_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_7_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_8_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_9_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_10_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_11_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_12_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_13_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_14_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_KLASSE_LED_15_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Binningklasse am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_1_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_2_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_3_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_4_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_5_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_6_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_7_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_8_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_9_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_10_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_11_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_12_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_13_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_14_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_WIDERSTAND_LED_15_WERT | kOhm | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Binningwiderstand am jeweiligen LED-Ausgang. |
| STAT_BINNING_SPANNUNG_LED_1_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_2_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_3_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_4_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_5_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_6_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_7_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_8_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_9_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_10_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_11_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_12_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_13_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_14_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |
| STAT_BINNING_SPANNUNG_LED_15_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am jeweiligen Binningwiderstand des jeweiligen LED-Ausgangs. |

<a id="table-res-0xd9f9-d"></a>
### RES_0XD9F9_D

Dimensions: 45 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_NTC_TEMPERATUR_LED_1_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_2_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_3_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_4_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_5_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_6_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_7_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_8_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_9_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_10_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_11_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_12_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_13_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_14_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_TEMPERATUR_LED_15_WERT | °C | high | unsigned char | - | - | 1.0 | 1.0 | -40.0 | NTC Temperatur des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_DEGRADATIONSLEVEL_LED_1_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_2_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_3_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_4_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_5_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_6_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_7_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_8_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_9_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_10_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_11_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_12_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_13_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_14_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_DEGRADATIONSLEVEL_LED_15_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Thermomanagementklasse bzw. Degradationslevel des jeweiligen LED-Ausgangs bzw. Lichtfunktion. |
| STAT_NTC_SPANNUNG_LED_1_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_2_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_3_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_4_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_5_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_6_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_7_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_8_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_9_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_10_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_11_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_12_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_13_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_14_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |
| STAT_NTC_SPANNUNG_LED_15_WERT | V | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Anliegende Spannung am NTC des jeweiligen LED-Ausgangs bzw. LED-Moduls. |

<a id="table-res-0xd9fa-d"></a>
### RES_0XD9FA_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZIERUNG_AHL | 0-n | high | unsigned char | - | REFERENZIERUNG_SCHRITTMOTOR | - | - | - | Status Referenzierung |
| STAT_POSITION_AHL_WERT | ° | high | unsigned int | - | - | 1.0 | 5.0 | -40.0 | Gibt die aktuelle Position des Schrittmotors AHL in ° (Grad) an. |

<a id="table-res-0xd9fb-d"></a>
### RES_0XD9FB_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REFERENZIERUNG_LWR | 0/1 | high | unsigned char | - | - | - | - | - | 0: NICHT REFERENZIERT 1: REFERENZIERT |
| STAT_POSITION_LWR_WERT | ° | high | unsigned int | - | - | 1.0 | 5.0 | -40.0 | Gibt die aktuelle Position des Schrittmotors LWR in ° (Grad) an. |

<a id="table-res-0xd9fc-d"></a>
### RES_0XD9FC_D

Dimensions: 69 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ABBLENDLICHT_1_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_2_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_3_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_4_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_1_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_2_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_3_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_4_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_5_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_6_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_7_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_8_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_9_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_10_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_1_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_2_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_3_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_4_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_BLINKER_1_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_SEITENMARKIERUNGSLICHT_1_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_LASER_1_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_LASERINSZENIERUNG_1_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_LASERINSZENIERUNG_2_LED_AUSGANG_WERT | - | high | unsigned char | - | - | 1.0 | 10.0 | 0.0 | Ausgabe des phys. LED-Ausgang zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_1_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_2_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_3_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_4_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_1_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_2_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_3_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_4_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_5_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_6_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_7_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_8_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_9_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_10_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_1_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_2_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_3_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_4_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_BLINKER_1_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_SEITENMARKIERUNGSLICHT_1_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_LASER_1_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_LASERINSZENIERUNG_1_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_LASERINSZENIERUNG_2_BINNING_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs Binning zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_1_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_2_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_3_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_ABBLENDLICHT_4_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_1_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_2_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_3_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_4_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_5_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_6_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_7_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_8_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_9_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_FERNLICHT_10_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_1_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_2_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_3_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_TAGFAHRLICHT_STANDLICHT_4_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_BLINKER_1_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_SEITENMARKIERUNGSLICHT_1_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_LASER_1_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_LASERINSZENIERUNG_1_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |
| STAT_LASERINSZENIERUNG_2_NTC_EINGANG_WERT | - | high | unsigned char | - | - | 1.0 | 1.0 | 0.0 | Ausgabe des phys. Sensoreingangs NTC zum jeweiligen Leuchtmittel. |

<a id="table-res-0xda71-d"></a>
### RES_0XDA71_D

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Bit | high | BITFIELD | - | BF_FAHRZEUG_ENTWICKLUNGSBEZEICHNUNG | - | - | - | Ausgabe der Fahrzeugvariante (BMW Entwicklungscode) und LCI |
| - | Bit | high | BITFIELD | - | BF_SCHEINWERFER_TYP | - | - | - | Ausgabe des Scheinwerfertyps:  - SA-Variante/-Bezeichnung - Ländervariante - Hersteller |
| STAT_SCHEINWERFER_VERSIONSNUMMER_WERT | HEX | high | unsigned char | - | - | - | - | - | Scheinwerferprojekt-Variante: Scheinwerfer Lebenslauf (Versionsnummer) |
| STAT_SG_VARIANTE_DATA | DATA | high | data[8] | - | - | 1.0 | 1.0 | 0.0 | Ausgabe der SG-Bestückvariante |
| STAT_SG_VARIANTE_GUELTIGKEIT | 0/1 | high | unsigned char | - | - | - | - | - | Ausgabe Gültigkeit der Variantendaten 0x00: ungültig, Default-Daten werden verwendet 0x01: gültig |
| STAT_SG_PRODUKTIONSSTANDORT_WERT | HEX | high | unsigned char | - | - | - | - | - | 0x00: DEUTSCHLAND / KRONACH  0x01: MEXIKO / APODACA |

<a id="table-res-0xda72-d"></a>
### RES_0XDA72_D

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHEINWERFER_DATEN_DATA | DATA | high | data[16] | - | - | 1.0 | 1.0 | 0.0 | Scheinwerferspezifische Daten |

<a id="table-res-0xdac8-d"></a>
### RES_0XDAC8_D

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HIGHSIDE_KURZSCHLUSS_ABSCHALTUNG_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Byte 1/2 = HSS1/2, Byte 3 = SBC:  0=nicht abgeschaltet, 1=abgeschaltet |
| STAT_HIGHSIDE_KURZSCHLUSS_ZAEHLER_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Byte 1/2 = HSS1/2  Byte 3 = SBC |
| STAT_HIGHSIDE_KURZSCHLUSS_WIEDERHOL_ZAEHLER_DATA | DATA | high | data[3] | - | - | 1.0 | 1.0 | 0.0 | Byte 1/2 = HSS1/2  Byte 3 = SBC |

<a id="table-res-0xe3ee-d"></a>
### RES_0XE3EE_D

Dimensions: 14 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BINNINGDATEN_LINKS_DATA | DATA | high | data[5] | - | - | 1.0 | 1.0 | 0.0 | Binningdaten Leuchtmittel inkl. Checksumme Scheinwerfer links |
| STAT_BINNINGDATEN_RECHTS_DATA | DATA | high | data[5] | - | - | 1.0 | 1.0 | 0.0 | Binningdaten Leuchtmittel inkl. Checksumme Scheinwerfer rechts |
| STAT_BINNINGWERT_LM_1_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_2_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_3_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_4_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_5_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_6_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_7_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_8_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_9_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_10_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_11_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |
| STAT_BINNINGWERT_LM_12_WERT | HEX | high | unsigned char | - | - | - | - | - | Binningwert des Leuchtmittels X der aktuellen Fahrzeugseite DEZ [0..4], HEX [0x00..0x04] |

<a id="table-res-0xf001-r"></a>
### RES_0XF001_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_REGISTER_WERT | + | - | - | HEX | high | unsigned char | - | - | - | - | - | Inhalt des Registers |

<a id="table-res-0xf152-d"></a>
### RES_0XF152_D

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HW_MODIFICATION_INDEX_WERT | HEX | high | unsigned char | - | - | - | - | - | Index of hardware modification:  FF: Not supported index |
| - | Bit | high | BITFIELD | - | BF_22_F152_SUPPLIERINFO | - | - | - | Tab Supplierinfo |

<a id="table-scheinwerfer-hersteller"></a>
### SCHEINWERFER_HERSTELLER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x20 | AUTOMOTIVE LIGHTING |
| 0x60 | HELLA |
| 0x80 | ZKW |
| 0xA0 | VALEO |
| 0xFF | Wert ungültig |

<a id="table-scheinwerfer-laender-variante"></a>
### SCHEINWERFER_LAENDER_VARIANTE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ECE |
| 1 | US |
| 0xFF | Wert ungültig |

<a id="table-scheinwerfer-sa-variante"></a>
### SCHEINWERFER_SA_VARIANTE

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE SA |
| 0x02 | 524 (ADAPTIVES KURVENLICHT) |
| 0x04 | 552 (ADAPTIVER LED SCHEINWERFER) |
| 0x06 | 552 (ADAPTIVER LED SCHEINWERFER MATRIX) |
| 0x08 | 5A2 (LED SCHEINWERFER) |
| 0x0A | 5A4 (LED SCHEINWERFER MIT ERWEITERTEN FUNKTIONEN) |
| 0x0C | 5AZ (LASERLICHT SCHEINWERFER) |
| 0xFF | Wert ungültig |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 67 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PROGRAMMING_COUNTER | 0x2502 | - | Programming-Counter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2502_D |
| PROGRAMMING_COUNTER_MAX_VALUE | 0x2503 | STAT_PROG_MAX_WERT | maximalen Anzahl von Programmiervorgängen | - | - | High | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| FLASH_TIMING_PARAMETER | 0x2504 | - | Programmierspezifische Timing Parameter | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2504_D |
| MILE_KM_EEPROM | 0x2540 | STAT_MILE_KM_EEPROM_DATA | Im EEPROM abgelegter Kilometerstand. | DATA | - | High | data[3] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _READ_HW_VARIANT | 0x4040 | - | Liest die kodierte HW-VAriante aus dem Steuergerät aus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4040_D |
| _READ_SCHRITTMOTOR_POSITION | 0x4041 | - | Liest die aktuelle Schrittmorposition aus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4041_D |
| _READ_STATUS_SCHRITTMOTOR | 0x4042 | - | Liest den aktuellen Stus der Schrittmotoren aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4042_D |
| _SCHRITTMOTOREN_REFERENZLAUF | 0x4044 | - | Startet den REferenzlauf des gewählten Schrittmotors | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4044_D | - |
| _SCHRITTMOTOR_POSITION | 0x4045 | - | Fährt den ausgewählten Schrittmotor zur angeforderten Position unter Angabe der Mikrosekunden pro Schritt | - | - | - | - | - | - | - | - | - | 2E | ARG_0x4045_D | - |
| _IC_TEMPERATUR_LIFETIME | 0x4046 | - | Liefert das Temperaturhistogramm der Treiber-ICs über die Lebenszeit des Steuergereätes | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4046_D |
| _IC_TEMPERATUR_ZYKLUS | 0x4047 | - | Liefert das Histogramm der Treiber-ICs seit dem letzten Aufstart zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4047_D |
| _STATUS_IC_TEMPERATUR_AKTUELL | 0x4048 | - | Liefert die aktuellen Temperaturen der einzelnen Treiber ICs zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4048_D |
| _STATUS_ANALOG_INPUTS | 0x4049 | - | Liefert den Rohwert der analogen Eingänge zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4049_D |
| _PCB_SERIAL_NUMBER | 0x404A | STAT_PCB_SERIAL_NUMBER_DATA | Seriennummer der Leiterplatte | DATA | - | High | data[12] | - | 1.0 | 1.0 | 0.0 | - | 22 | - | - |
| _LED_DRIVER_CONFIGURATION | 0x404B | - | Gibt die Werte der Shuntwiderstände der LED-Treiber zurück | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x404B_D |
| _LED_CURRENT | 0x404C | - | setzt den eingestellten Strom der LED-Ausgänge. Nach Timeout wird wieder der kodierte Strom verwendet | - | - | - | - | - | - | - | - | - | 2E | ARG_0x404C_D | - |
| _LAST_FUSI_RESET | 0x404D | - | gibt die Ursache des letzten Resets an, der durch Fusi getriggert wurde | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x404D_D |
| _RESET_LAST_FUSI_RESET | 0x404E | - | löscht die Informationen des letzten Resets der durch Fusi getriggert wurde | - | - | - | - | - | - | - | - | - | 2E | ARG_0x404E_D | - |
| _LED_TREIBER_KALIBRIERUNG | 0x4051 | - | Auslesender Kalibrierdaten der LED-Treiber | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4051_D |
| FLM_FUNKTIONSTEST | 0xA549 | - | Funktionstest LED Scheinwerfer | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA549_R |
| FLM_FUNKTIONSTEST_LASER | 0xA54A | - | Funktionstest Laserscheinwerfer | - | - | - | - | - | - | - | - | - | 31 | - | RES_0xA54A_R |
| FLM_KANAL | 0xA54B | - | Ansteuerung einzelner oder aller LED-Kanäle. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA54B_R | - |
| SATELLIT_UDS_TRANSFER | 0xA54C | - | Tunnel-Job UDS für Diagnose FLM Satelliten-Elektronik | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA54C_R | RES_0xA54C_R |
| FLM_LUEFTER | 0xA54D | - | Einschalten des Lüfters für eine bestimmte Periode von 1..254 Sekunden oder dauerhaft. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA54D_R | RES_0xA54D_R |
| FLM_POSITION_AHL | 0xA54E | - | Steuern der Position des Schrittmotors AHL | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA54E_R | RES_0xA54E_R |
| FLM_POSITION_LWR | 0xA54F | - | Steuern der Position des Schrittmotors LWR | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA54F_R | RES_0xA54F_R |
| FLM_HIGHSIDE_SCHALTER | 0xA550 | - | Ansteuerung einzelner Highside Switch Ausgänge. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xA550_R | - |
| FLM_BINNINGDATEN_LEUCHTE | 0xACDC | - | Diagnosejob Binning-Informationen Schreiben/Lesen für speicherbasierte Binninginformationen. | - | - | - | - | - | - | - | - | - | 31 | - | - |
| FLM_KURZSCHLUSS_SCHALTER | 0xAFF3 | - | Gibt an, welcher KSS bitcodiert geschlossen werden soll | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAFF3_R | RES_0xAFF3_R |
| FLM_SCHRITTVERLUSTE_AHL | 0xD6D3 | - | Zähler der Schrittverluste des AHL Schrittmotors. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6D3_D |
| FLM_SCHRITTVERLUSTE_AHL_LOESCHEN | 0xD6D4 | - | Löschen des Zählers Schrittverluste für AHL Schrittmotor. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD6D4_D | - |
| FLM_KANAL_ERGEBNISSE | 0xD6DB | - | Ergebnisse zur Ansteuerung einzelner oder aller LED-Kanäle. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6DB_D |
| FLM_FUNKTION_LICHTVERTEILUNG | 0xD6DC | - | Funktionale Ansteuerung der FLM Funktionen bzw. Lichtverteilungen Frontlicht | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD6DC_D | - |
| FLM_HIGHSIDE_SCHALTER_ERGEBNISSE | 0xD6DF | - | Ausgabe der PWM, Strom und Spannung der Highside Schalter. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD6DF_D |
| FLM_FUNKTION_LICHTVERTEILUNG_ERGEBNISSE | 0xD7A7 | - | Funktionale Ansteuerung der FLM Funktionen | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7A7_D |
| FLM_HIGHSIDE_SCHALTER_RESET | 0xD7AB | - | Reset der am Highsideschalter angeschlossenen Peripherie durch Öffnen des Schalters | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD7AB_D | - |
| FLM_BETRIEBSDAUER_LOESCHEN | 0xD7AC | - | Löschen der Betriebsdauern aller Komponenten des Steuergeräts (Kanäle, Lüfter, Schrittmotoren, Highsideswitch, Kurzschlussschalter, etc.) | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD7AC_D | - |
| FLM_BETRIEBSDAUER | 0xD7AD | - | Gibt die Betriebsdauer aller Komponenten des Steuergeräts an.  (Kanäle, Lüfter, Schrittmotoren, Highsideswitch, Kurzschlussschalter, etc.) | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7AD_D |
| FLM_RESET_ZAEHLER_LOESCHEN | 0xD7B9 | - | Löschen des Steuergeräte-Resetzählers. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD7B9_D | - |
| FLM_RESET_ZAEHLER | 0xD7BA | - | Ausgabe Anzahl der Resetvorgänge des Steuergeräts. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7BA_D |
| FLM_REFERENZLAUF_ZAEHLER_AHL_LOESCHEN | 0xD7BB | - | Löschen des Referenzlaufzählers für den AHL Schrittmotor. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD7BB_D | - |
| FLM_REFERENZLAUF_ZAEHLER_AHL | 0xD7BC | - | Anzahl der begonnenen und abgeschlossenen Referenzläufe des AHL Schrittmotors. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7BC_D |
| FLM_REFERENZLAUF_ZAEHLER_LWR_LOESCHEN | 0xD7BD | - | Löschen des Referenzlaufzählers für den LWR Schrittmotor. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD7BD_D | - |
| FLM_REFERENZLAUF_ZAEHLER_LWR | 0xD7BE | - | Anzahl der begonnenen und abgeschlossenen Referenzläufe des LWR Schrittmotors. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD7BE_D |
| FLM_EINGANGSSPANNUNG | 0xD9BC | STAT_SPANNUNG_KLEMME_LICHT_WERT | Eingangsspannung Steuergerät | V | - | High | unsigned char | - | 1.0 | 10.0 | 0.0 | - | 22 | - | - |
| FLM_FRAZ_FEEDBACK | 0xD9BD | - | Ausgabe des Stromwerts und PWM des LED-Ausgangs für Blinker. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9BD_D |
| FLM_TEMPERATURHISTOGRAMM_LOESCHEN | 0xD9BE | - | Löschen des Temperaturhistogramms im Steuergerät. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD9BE_D | - |
| FLM_TEMPERATURHISTOGRAMM | 0xD9BF | - | Ausgabe der Temperaturhistogramme | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9BF_D |
| SATELLIT_LASER_KOMMUNIKATION | 0xD9C8 | - | Gibt die Statusbotschaften des Lasersatelliten auf dem Private-CAN aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9C8_D |
| FLM_TEMPERATURMODUS_AHL | 0xD9F6 | - | Ausgabe des aktuellen Modus für Schrittmotor AHL:  Tieftemperaturmodus, Normalmodus, Hochtemperaturmodus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9F6_D |
| FLM_TEMPERATURMODUS_LWR | 0xD9F7 | - | Ausgabe des aktuellen Modus für Schrittmotor LWR:  Tieftemperaturmodus, Normalmodus, Hochtemperaturmodus | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9F7_D |
| FLM_BINNING_DATEN | 0xD9F8 | - | Ausgabe der Binningdaten: - Binningklasse  - Binningwiderstand  - anliegende Spannung am RBIN | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9F8_D |
| FLM_NTC_DATEN | 0xD9F9 | - | Ausgabe der NTC-Daten:  - Erkannte Temperatur  - Thermomanagementklasse / Degradationslevel  - anliegende Spannung am RNTC | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9F9_D |
| FLM_REFERENZIERUNG_AHL | 0xD9FA | - | Gibt den Referenzstatus des AHL Schrittmotors und die aktuelle Stellung aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9FA_D |
| FLM_REFERENZIERUNG_LWR | 0xD9FB | - | Gibt den Referenzstatus des LWR Schrittmotors und die aktuelle Stellung aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9FB_D |
| FLM_ZUORDUNG_SENSOREN_KANAELE | 0xD9FC | - | Ausgabe der Zuordnung: - phys. LED-Ausgang zu Leuchtmittel  - phys. Ausgang BIN/NTC zu Leuchtmittel | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xD9FC_D |
| FLM_REFERENZIERUNG_SCHRITTMOTOR | 0xD9FD | - | Referenzlauf für Schrittmotoren LWR oder AHL anstoßen oder in Abstellposition fahren | - | - | - | - | - | - | - | - | - | 2E | ARG_0xD9FD_D | - |
| SCHEINWERFER_VARIANTE | 0xDA71 | - | Lesen der Fahrzeug, Scheinwerfer und Steuergeräte Variantenkennung aus den Codierdaten | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDA71_D |
| SCHEINWERFER_DATEN | 0xDA72 | - | Daten, die bei der Scheinwerferfertigung im Steuergerät abgelegt werden | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDA72_D | RES_0xDA72_D |
| FLM_HIGHSIDE_RESET_KURZSCHLUSS_ABSCHALTUNG | 0xDAC5 | - | Rücksetzen der Kurzschlussabschaltung einzelner Highside-Schalter | - | - | - | - | - | - | - | - | - | 2E | ARG_0xDAC5_D | - |
| FLM_HIGHSIDE_KURZSCHLUSS_ABSCHALTUNG_ZAEHLER | 0xDAC8 | - | Status Highsideswitch Kurzschluss - Abschaltung - Zähler - Wiederholzähler | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDAC8_D |
| FLM_BINNINGDATEN_LEUCHTE_SCHREIBEN | 0xE3ED | - | Binningdaten für die tauschbaren Leuchtmittel schreiben. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xE3ED_D | - |
| FLM_BINNINGDATEN_LEUCHTE_LESEN | 0xE3EE | - | Liest die Binningdaten der tauschbaren Leuchtmittel aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xE3EE_D |
| _LESEN_LED_TREIBER_REGISTER | 0xF001 | - | Lessen des Inhalts eines LED-Treiberregisters | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF001_R | RES_0xF001_R |
| _FUSI_TEST | 0xF002 | - | Testet Reset-Funktionalität des FLM | - | - | - | - | - | - | - | - | - | 31 | ARG_0xF002_R | - |
| READHWMODIFICATIONINDEX | 0xF152 | - | Dieser Service kommt nur zum Einsatz, wenn es eine geringfügige Hardwareänderung an dem Steuergerät gegeben hat, die nicht zu einer Änderung der Sachnummer bzw. der Hardware SGBM-IDs geführt hat. Eine solche Änderung ist von außen nicht diagnostizierbar, daher wurde dieser Dienst dafür eingeführt. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF152_D |
| ACTIVE_DIAGNOSTIC_SESSION | 0xF186 | STAT_ACTIVE_DIAGNOSTIC_SESSION | activeDiagnosticSession | 0-n | - | High | unsigned char | RDBI_ADS_DOP | - | - | - | - | 22 | - | - |

<a id="table-tab-flm-highside-switch"></a>
### TAB_FLM_HIGHSIDE_SWITCH

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Aktion |
| 0x01 | Highside Schalter 1: SAT/LAMPE |
| 0x02 | Highside Schalter 2: SAT/LAMPE |
| 0x03 | Highside Schalter 3: LUEFTER |
| 0x04 | alle Highside Schalter |

<a id="table-tab-flm-kanal-arg"></a>
### TAB_FLM_KANAL_ARG

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | alle |
| 0x01 | Kanal 1 |
| 0x02 | Kanal 2 |
| 0x03 | Kanal 3 |
| 0x04 | Kanal 4 |
| 0x05 | Kanal 5 |
| 0x06 | Kanal 6 |
| 0x07 | Kanal 7 |
| 0x08 | Kanal 8 |
| 0x09 | Kanal 9 |
| 0x0A | Kanal 10 |
| 0x0B | Kanal 11 |
| 0x0C | Kanal 12 |
| 0x0D | Kanal 13 |
| 0x0E | Kanal 14 |
| 0x0F | Kanal 15 |

<a id="table-tab-lf-lv-front-arg"></a>
### TAB_LF_LV_FRONT_ARG

Dimensions: 78 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Abblendlicht LV1 - Schlechtwetter C1 |
| 0x02 | Abblendlicht LV2 - Schlechtwetter C2 |
| 0x03 | Abblendlicht LV3 - Stadt V |
| 0x04 | Abblendlicht LV4 - SAE |
| 0x05 | Abblendlicht LV5 - H10 Landstrasse C |
| 0x06 | Abblendlicht LV6 - H8 Autobahn E3 |
| 0x07 | Abblendlicht LV7 - H6 Autobahn E2 |
| 0x08 | Abblendlicht LV8 - H5 Autobahn E1 |
| 0x09 | Abblendlicht LV9 - H4 Autobahn E |
| 0x0A | Abblendlicht LV10 - H2 |
| 0x0B | Abblendlicht LV11 - H0 |
| 0x0C | Abblendlicht LV12 - H plus 2 |
| 0x0D | Abblendlicht LV13 - H plus 4 |
| 0x0E | Abblendlicht LV14 - Blendfreies Fernlicht |
| 0x0F | Abblendlicht LV15a - Fernlicht Modus 1a |
| 0x10 | Abblendlicht LV15b - Fernlicht Modus 1b |
| 0x11 | Abblendlicht LV16a - Fernlicht Modus 2a |
| 0x12 | Abblendlicht LV16b - Fernlicht Modus 2b |
| 0x13 | Abblendlicht LV17a - Fernlicht Modus 3a |
| 0x14 | Abblendlicht LV17b - Fernlicht Modus 3b |
| 0x15 | Abblendlicht LV18 - Blendfreies Fernlicht 1 |
| 0x16 | Abblendlicht LV19 - Blendfreies Fernlicht 2 |
| 0x17 | Abblendlicht LV20a - Blendfreies Fernlicht 3a |
| 0x18 | Abblendlicht LV20b - Blendfreies Fernlicht 3b |
| 0x19 | Abblendlicht LV21 - Blendfreies Fernlicht 4 |
| 0x1A | Abblendlicht LV22 - Matrix Haupt |
| 0x1B | Abblendlicht LV22.01 - Matrix 1 |
| 0x1C | Abblendlicht LV22.02 - Matrix 2 |
| 0x1D | Abblendlicht LV22.03 - Matrix 3 |
| 0x1E | Abblendlicht LV22.04 - Matrix 4 |
| 0x1F | Abblendlicht LV22.05 - Matrix 5 |
| 0x20 | Abblendlicht LV22.06 - Matrix 6 |
| 0x21 | Abblendlicht LV22.07 - Matrix 7 |
| 0x22 | Abblendlicht LV22.08 - Matrix 8 |
| 0x23 | Abblendlicht LV22.08 - Matrix 9 |
| 0x24 | Abblendlicht LV22.08 - Matrix 10 |
| 0x25 | Abblendlicht LV22.08 - Matrix 11 |
| 0x26 | Abblendlicht LV22.08 - Matrix 12 |
| 0x27 | Abblendlicht LV22.08 - Matrix 13 |
| 0x28 | Abblendlicht LV22.08 - Matrix 14 |
| 0x29 | Abblendlicht LV22.08 - Matrix 15 |
| 0x2A | Abblendlicht LV22.08 - Matrix 16 |
| 0x2B | Abblendlicht LV23 - Blendfreies Fernlicht 6 |
| 0x2C | Abblendlicht LV23 - Blendfreies Fernlicht 7 |
| 0x2D | Abblendlicht LV23 - Blendfreies Fernlicht 8 |
| 0x2E | Abblendlicht LV23 - Blendfreies Fernlicht 9 |
| 0x2F | Abblendlicht LV23 - Blendfreies Fernlicht 10 |
| 0x30 | Abblendlicht LV23 - Blendfreies Fernlicht 11 |
| 0x31 | Abblendlicht LV23 - Blendfreies Fernlicht 12 |
| 0x32 | Abblendlicht LV23 - Blendfreies Fernlicht 13 |
| 0x33 | Tagfahrlicht |
| 0x34 | Abbiegelicht |
| 0x35 | Standlicht Modus 1 |
| 0x36 | Standlicht Modus 2 |
| 0x37 | Standlicht Modus 3 |
| 0x38 | Parklicht |
| 0x39 | Welcome Light Modus 1 |
| 0x3A | Welcome Light Modus 2 |
| 0x3B | Welcome Light Modus 3 |
| 0x3C | Welcome Light Modus 4 |
| 0x3D | Welcome Light Modus 5 |
| 0x3E | Follow Me Home |
| 0x3F | Remote Light |
| 0x40 | Goodbye Light Modus 1 |
| 0x41 | Goodbye Light Modus 2 |
| 0x42 | Goodbye Light Modus 3 |
| 0x43 | Goodbye Light Modus 4 |
| 0x44 | Goodbye Light Modus 5 |
| 0x45 | Fernlichtblinken |
| 0x46 | Überfallalarm |
| 0x47 | DWA-Blinken |
| 0x48 | Panik-Modus |
| 0x49 | Blinken |
| 0x4A | Blinken 2 |
| 0x4B | ECO+ Dimmung 1 |
| 0x4C | ECO+ Dimmung 2 |
| 0x4D | ECO+ Dimmung 3 |
| 0x4E | SML |

<a id="table-tab-supplierinfo-field"></a>
### TAB_SUPPLIERINFO_FIELD

Dimensions: 64 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Wert 0 |
| 0x1 | Wert 1 |
| 0x2 | Wert 2 |
| 0x3 | Wert 3 |
| 0x4 | Wert 4 |
| 0x5 | Wert 5 |
| 0x6 | Wert 6 |
| 0x7 | Wert 7 |
| 0x8 | Wert 8 |
| 0x9 | Wert 9 |
| 0xA | Wert 10 |
| 0xB | Wert 11 |
| 0xC | Wert 12 |
| 0xD | Wert 13 |
| 0xE | Wert 14 |
| 0xF | Wert 15 |
| 0x10 | Wert 16 |
| 0x11 | Wert 17 |
| 0x12 | Wert 18 |
| 0x13 | Wert 19 |
| 0x14 | Wert 20 |
| 0x15 | Wert 21 |
| 0x16 | Wert 22 |
| 0x17 | Wert 23 |
| 0x18 | Wert 24 |
| 0x19 | Wert 25 |
| 0x1A | Wert 26 |
| 0x1B | Wert 27 |
| 0x1C | Wert 28 |
| 0x1D | Wert 29 |
| 0x1E | Wert 30 |
| 0x1F | Wert 31 |
| 0x20 | Wert 32 |
| 0x21 | Wert 33 |
| 0x22 | Wert 34 |
| 0x23 | Wert 35 |
| 0x24 | Wert 36 |
| 0x25 | Wert 37 |
| 0x26 | Wert 38 |
| 0x27 | Wert 39 |
| 0x28 | Wert 40 |
| 0x29 | Wert 41 |
| 0x2A | Wert 42 |
| 0x2B | Wert 43 |
| 0x2C | Wert 44 |
| 0x2D | Wert 45 |
| 0x2E | Wert 46 |
| 0x2F | Wert 47 |
| 0x30 | Wert 48 |
| 0x31 | Wert 49 |
| 0x32 | Wert 50 |
| 0x33 | Wert 51 |
| 0x34 | Wert 52 |
| 0x35 | Wert 53 |
| 0x36 | Wert 54 |
| 0x37 | Wert 55 |
| 0x38 | Wert 56 |
| 0x39 | Wert 57 |
| 0x3A | Wert 58 |
| 0x3B | Wert 59 |
| 0x3C | Wert 60 |
| 0x3D | Wert 61 |
| 0x3E | Wert 62 |
| 0xFF | Wert ungültig |
