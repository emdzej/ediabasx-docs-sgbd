# mrabs2.prg

- Jobs: [50](#jobs)
- Tables: [25](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRABS2 |
| ORIGIN | BMW UX-ER-4 Anton Mayer |
| REVISION | 1.002 |
| AUTHOR | BMW_AG UX-EE-1 Krimmer |
| COMMENT | fuer Bosch-ABS 8M in K15 und R13, aus MRABS erstellt |
| PACKAGE | 1.50 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [STEUERN_FG](#job-steuern-fg) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [SUPPLIER_SW_NUMBER](#job-supplier-sw-number) - Reads the system supplier ECU software number KWP2000: $1A Ecu Identification $94 SystemSupplierECUSoftwareNumber Modus: Default
- [SUPPLIER_HW_NUMBER](#job-supplier-hw-number) - Reads the system supplier ECU hardware number KWP2000: $1A Ecu Identification $92 SystemSupplierECUHardwareNumber Modus: Default
- [SUPPLIER_SW_VERSION_NUMBER](#job-supplier-sw-version-number) - Reads the supplier software version number KWP2000: $1A Ecu Identification $95 Robert Bosch ECU software version number Modus: Default
- [STATUS_WHEEL_SPEED](#job-status-wheel-speed) - Reads front and rear wheel speed KWP2000: $21 ReadDataByLocalIdentifier $01 Wheel Speed Modus: Default
- [STATUS_ANALOG_INPUT](#job-status-analog-input) - Read analog input signals KWP2000: $21 ReadDataByLocalIdentifier $02 Analog input signals Modus: Default
- [STEUERN_EVAC_AND_FILL](#job-steuern-evac-and-fill) - Note: The valve protection for the AVs is switched off during this test Therefore the test should not be repeated too often in case of a long control duration KWP2000: $30 InputOutputControlByLocalId $01 Local ID EvacAndFill $07 InputOutputControlParameter Modus:        Default
- [STATUS_EVAC_AND_FILL](#job-status-evac-and-fill) - Read status Evac and Fill KWP2000:      $33 RequestRoutingResultsByLocalId $01 EvacAndFill Modus:        Default
- [STEUERN_REPAIR_BLEEDING](#job-steuern-repair-bleeding) - Note: The phase must always begin with the 1.phase and be processed in ascending order It is permitted to repeat the same phase. However no phase may be skipped. If it is disregarded, the pump can be damaged by dry running. KWP2000: $30 InputOutputControlByLocalId $02 Local ID Repair Bleeding $07 InputOutputControlParameter Modus:        Default
- [STATUS_REPAIR_BLEEDING](#job-status-repair-bleeding) - Read status Repair Bleeding KWP2000:      $33 RequestRoutingResultsByLocalId $02 RepairBleeding Modus:        Default
- [STEUERN_SPEED_SENSOR_TEST](#job-steuern-speed-sensor-test) - Activating of the speed sensor test KWP2000: $30 InputOutputControlByLocalId $03 Local ID speed sensor test $07 InputOutputControlParameter Modus:        Default
- [STATUS_SPEED_SENSOR_TEST](#job-status-speed-sensor-test) - Read status SpeedSensorTest KWP2000:      $33 RequestRoutingResultsByLocalId $03 SpeedSensorTest Modus:        Default
- [STEUERN_ACTUATOR_TEST](#job-steuern-actuator-test) - Activating of the acutator test KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Modus:        Default
- [STATUS_ACTUATOR_TEST](#job-status-actuator-test) - Read status ActuatorTest KWP2000:      $33 RequestRoutineResultsByLocalId $04 ActuatorTest Modus:        Default
- [STEUERN_DYNAMIC_TEST](#job-steuern-dynamic-test) - Activating of the dynamic test KWP2000: $30 InputOutputControlByLocalId $04 Local ID dynamic test $07 InputOutputControlParameter Modus:        Default
- [STATUS_DYNAMIC_TEST](#job-status-dynamic-test) - Read status DynamicTest KWP2000:      $33 RequestRoutineResultsByLocalId $05 DynamicTest Modus:        Default
- [STEUERN_WSS_FRONT_MISSING_TEETH_TEST](#job-steuern-wss-front-missing-teeth-test) - Activating front missing teeth test KWP2000: $30 InputOutputControlByLocalId $06 Front missing teeth test $07 InputOutputControlParameter Modus:        Default
- [STATUS_WSS_FRONT_MISSING_TEETH_TEST](#job-status-wss-front-missing-teeth-test) - Status Missing teeth test KWP2000:      $33 RequestRoutingResultsByLocalId $06 WSSFrontMissingTeethTest Modus:        Default
- [STEUERN_WSS_REAR_MISSING_TEETH_TEST](#job-steuern-wss-rear-missing-teeth-test) - Activating rear missing teeth test KWP2000: $30 InputOutputControlByLocalId $06 Rear missing teeth test $07 InputOutputControlParameter Modus:        Default
- [STATUS_WSS_REAR_MISSING_TEETH_TEST](#job-status-wss-rear-missing-teeth-test) - Status Missing teeth test KWP2000:      $33 RequestRoutingResultsByLocalId $07 WSSRearMissingTeethTest Modus:        Default
- [STEUERN_STOP_ACTUATION](#job-steuern-stop-actuation) - KWP2000: $30 InputOutputControlByLocalId $10 Local ID StopActuation $07 InputOutputControlParameter Modus:        Default
- [STEUERN_RETURN_PUMP](#job-steuern-return-pump) - Activating the return pump KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default
- [STEUERN_ALL_VALVES](#job-steuern-all-valves) - Activating all valves KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default
- [STEUERN_EV_FRONT](#job-steuern-ev-front) - Activating EV front KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default
- [STEUERN_EV_REAR](#job-steuern-ev-rear) - Activating EV rear KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default
- [STEUERN_AV_FRONT](#job-steuern-av-front) - Activating AV front KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default
- [STEUERN_AV_REAR](#job-steuern-av-rear) - Activating AV rear KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default
- [_STEUERN_TELEGRAMM_TEST](#job-steuern-telegramm-test) - Activating of the acutator test KWP2000: $30 InputOutputControlByLocalId $XX $07 InputOutputControlParameter Modus:        Default
- [STATUS_VARIANT](#job-status-variant) - Lesen der angelernten Variante KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet Modus:        Default
- [STATUS_DIGITAL_INPUT](#job-status-digital-input) - Read digital input signals KWP2000: $21 ReadDataByLocalIdentifier $03 digital input Modus: Default
- [STEUERN_VARIANTE_K15](#job-steuern-variante-k15) - Codierung Variante K15 KWP2000: $2E   WriteDataByCommonIdentifier $3000 CodingDataSet
- [STEUERN_VARIANTE_R13](#job-steuern-variante-r13) - Codierung Variante R13 KWP2000: $2E   WriteDataByCommonIdentifier $3000 CodingDataSet

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

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardware-Versionsindex |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_VAR_INDEX | int | Varianten-Index |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| ID_SG_ADR | long | Steuergeraeteadresse bzw. LIN Master Steuergeraeteadresse |
| ID_LIN_SLAVE_ADR | long | LIN Slave Steuergeraeteadresse |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle Nur fuer DS2-Bordnetz benoetigt Fuer EWS-DME/DDE Abgleich |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | 0x????: Angabe eines einzelnen Fehlers 0xFFFB: alle Antriebsfehler 0xFFFC: alle Fahrwerkfehler 0xFFFD: alle Karosseriefehler 0xFFFE: alle Netzwerkfehler Default: 0xFFFF: alle Fehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |
| BAUDRATE | string | optionaler Parameter fuer die gewuenschte Baudrate table BaudRate BAUD |
| SPEZIFISCHE_BAUDRATE_WERT | long | Parameter nur fuer BAUDRATE = 'SB' ( spezifische Baudrate ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( 254 ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( max. 249 ) |
| DATEN | string | zu schreibende Daten (Anzahl siehe oben) z.B. 1,2,03,0x04,0x05... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fg"></a>
### STEUERN_FG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (17-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-supplier-sw-number"></a>
### SUPPLIER_SW_NUMBER

Reads the system supplier ECU software number KWP2000: $1A Ecu Identification $94 SystemSupplierECUSoftwareNumber Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_ALG | string | Bosch ECU BB-number Algorithm Server |
| SW_SYS | string | Bosch ECU BB-number System Server |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-supplier-hw-number"></a>
### SUPPLIER_HW_NUMBER

Reads the system supplier ECU hardware number KWP2000: $1A Ecu Identification $92 SystemSupplierECUHardwareNumber Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HW_NUMBER | string | Bosch ECU Hardware Number (TT-Number) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-supplier-sw-version-number"></a>
### SUPPLIER_SW_VERSION_NUMBER

Reads the supplier software version number KWP2000: $1A Ecu Identification $95 Robert Bosch ECU software version number Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_ALG | string | Bosch ECU SW Version Number Algorithm Server |
| SW_SYS | string | Bosch ECU SW Version Number System Server |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wheel-speed"></a>
### STATUS_WHEEL_SPEED

Reads front and rear wheel speed KWP2000: $21 ReadDataByLocalIdentifier $01 Wheel Speed Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FRONT_WHEEL_SPEED_VALUE | real | front wheel speed 0..337km/h |
| STAT_REAR_WHEEL_SPEED_VALUE | real | rear wheel speed 0..337km/h |
| STAT_WHEEL_SPEED_UNIT | string | km/h |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-input"></a>
### STATUS_ANALOG_INPUT

Read analog input signals KWP2000: $21 ReadDataByLocalIdentifier $02 Analog input signals Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KL15_VALUE | real | voltage KL15 0..20 [Volt] |
| STAT_KL15_UNIT | string | Volt |
| STAT_VALVE_RELAY_VALUE | real | valve relay voltage 0..20 [Volt] |
| STAT_VALVE_RELAY_UNIT | string | Volt |
| STAT_RETURN_PUMP_VALUE | real | Return pump 0..20 [Volt] |
| STAT_RETURN_PUMP_UNIT | string | Volt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-evac-and-fill"></a>
### STEUERN_EVAC_AND_FILL

Note: The valve protection for the AVs is switched off during this test Therefore the test should not be repeated too often in case of a long control duration KWP2000: $30 InputOutputControlByLocalId $01 Local ID EvacAndFill $07 InputOutputControlParameter Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACT_TIME | unsigned char | 0..150 [s] time &lt;= 150sec |
| DELAY_TIME | unsigned char | 0..254 [s] pump activation delay time the value 0 causes no pump activation |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-evac-and-fill"></a>
### STATUS_EVAC_AND_FILL

Read status Evac and Fill KWP2000:      $33 RequestRoutingResultsByLocalId $01 EvacAndFill Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EVAC_AND_FILL_TEXT | string | table Status_EvacFill_and_RepairBleeding |
| STAT_EVAC_AND_FILL_VALUE | unsigned char | table Status_EvacFill_and_RepairBleeding |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-repair-bleeding"></a>
### STEUERN_REPAIR_BLEEDING

Note: The phase must always begin with the 1.phase and be processed in ascending order It is permitted to repeat the same phase. However no phase may be skipped. If it is disregarded, the pump can be damaged by dry running. KWP2000: $30 InputOutputControlByLocalId $02 Local ID Repair Bleeding $07 InputOutputControlParameter Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PHASE | unsigned char | Phase 1 - 4 |
| REPETITION | unsigned char | Repetition 3 - 5 times (only in phase 2 and 4) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-repair-bleeding"></a>
### STATUS_REPAIR_BLEEDING

Read status Repair Bleeding KWP2000:      $33 RequestRoutingResultsByLocalId $02 RepairBleeding Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REPAIR_BLEEDING_TEXT | string | table Status_EvacFill_and_RepairBleeding |
| STAT_REPAIR_BLEEDING_VALUE | unsigned char | table Status_EvacFill_and_RepairBleeding |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-speed-sensor-test"></a>
### STEUERN_SPEED_SENSOR_TEST

Activating of the speed sensor test KWP2000: $30 InputOutputControlByLocalId $03 Local ID speed sensor test $07 InputOutputControlParameter Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DURATION | unsigned int | test duration 0..327 sec 100 = 1 sec, [10 msec] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-speed-sensor-test"></a>
### STATUS_SPEED_SENSOR_TEST

Read status SpeedSensorTest KWP2000:      $33 RequestRoutingResultsByLocalId $03 SpeedSensorTest Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MAX_SPEED_FRONT_VALUE | real | max wheel speed front 0..337km/h |
| STAT_MIN_SPEED_FRONT_VALUE | real | min wheel speed front 0..337km/h |
| STAT_MAX_SPEED_REAR_VALUE | real | max wheel speed rear 0..337km/h |
| STAT_MIN_SPEED_REAR_VALUE | real | min wheel speed rear 0..337km/h |
| STAT_WHEEL_SPEED_UNIT | string | km/h |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-actuator-test"></a>
### STEUERN_ACTUATOR_TEST

Activating of the acutator test KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA | binary | 18 DataBytes for Job control  *************************************************************** DATA_LAYOUT: ***************************************************************  \| Byte  \|  Contents                                \|  Value    \| --------------------------------------------------------------- 1,2      1.Activation value (HB,LB)                 xx xx (Hex) 3,4      1.Actuator number (HB,LB)                  xx xx (Hex) 5,6      2.Activation value (HB,LB)                 xx xx (Hex) 7,8      2.Actuator number (HB,LB)                  xx xx (Hex) 9,10     Waiting time between activations (HB,LB)   xx xx (Hex) .        resolution 10ms/Bit                        . 11,12    3.Activation value (HB,LB)                 xx xx (Hex) 13,14    3.Actuator number (HB,LB)                  xx xx (Hex) 15,16    4.Activation value (HB,LB)                 xx xx (Hex) 17,18    4.Actuator number (HB,LB)                  xx xx (Hex)    *************************************************************** ACTUATOR TABLE (see also Appendix A in specification): ***************************************************************  \|N°  \| Channel                     \| Resolution/Remarks (value) \| ---------------------------------------------------------------- 0000  No activation ---------------------------------------------------------------- 0022  Pump-motor relais             FFFF: on .     Return pump (MRA)             0000: off ---------------------------------------------------------------- 0028  Joint activation of all EVs   0 = not selected .     .                             1 = selected .     .                             Bit4: EV rear .     .                             Bit6: EV front .     .                             Bit8-15: Intensity in 1% per Bit .     .                                      00 = off .     .                                      01 - FF = on ---------------------------------------------------------------- 002A  Joint activation of all AVs   0 = not selected .     .                             1 = selected .     .                             Bit5: AV rear .     .                             Bit7: AV front .     .                             Bit8-15: Intensity in 1% per Bit .     .                                      00 = off .     .                                      01 - FF = on ---------------------------------------------------------------- 0030  EV front (EV-V)               0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 0032  AV front (AV-V)               0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 0038  EV rear (EV-H)                0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 003A  AV rear (AV-H)                0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 005E  Disable Valve-Protection      A5: disable shut down .     .                             00: enable shut down ---------------------------------------------------------------- 0064  Disable VR-shut down          A5: disable shut down .     .                             00: enable shut down ---------------------------------------------------------------- 0068  Disable abort of diagnosis    FF: disable shut down .     by speed limit                00: enable abort  Note: The AVs are used as a switch valve. When the activation value is not 0%, the software set it to 100% automatically |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-actuator-test"></a>
### STATUS_ACTUATOR_TEST

Read status ActuatorTest KWP2000:      $33 RequestRoutineResultsByLocalId $04 ActuatorTest Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ACT_1_VALUE | unsigned int | result of 1.Actuator |
| STAT_ACT_2_VALUE | unsigned int | result of 2.Actuator |
| STAT_ACT_3_VALUE | unsigned int | result of 3.Actuator |
| STAT_ACT_4_VALUE | unsigned int | result of 4.Actuator |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dynamic-test"></a>
### STEUERN_DYNAMIC_TEST

Activating of the dynamic test KWP2000: $30 InputOutputControlByLocalId $04 Local ID dynamic test $07 InputOutputControlParameter Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA | binary | 20 (!) DataBytes for Job Argument  *************************************************************** DATA_LAYOUT: ***************************************************************  \| Byte  \|  Contents                                \|  Value    \| --------------------------------------------------------------- 1,2      1.Activation value (HB,LB)                 xx xx (Hex) 3,4      1.Actuator number (HB,LB)                  xx xx (Hex) 5,6      2.Activation value (HB,LB)                 xx xx (Hex) 7,8      2.Actuator number (HB,LB)                  xx xx (Hex) 9,10     Waiting time between activations (HB,LB)   xx xx (Hex) .        resolution 10ms/Bit                        . 11,12    3.Activation value (HB,LB)                 xx xx (Hex) 13,14    3.Actuator number (HB,LB)                  xx xx (Hex) 15,16    4.Activation value (HB,LB)                 xx xx (Hex) 17,18    4.Actuator number (HB,LB)                  xx xx (Hex) 19,20    Waiting time after 2.activation (HB,LB)    xx xx (Hex) .        resolution 10ms/Bit                        .    *************************************************************** ACTUATOR TABLE (see also Appendix A in specification): ***************************************************************  \|N°  \| Channel                     \| Resolution/Remarks (value) \| ---------------------------------------------------------------- 0000  No activation ---------------------------------------------------------------- 0022  Pump-motor relais             FFFF: on .     Return pump (MRA)             0000: off ---------------------------------------------------------------- 0028  Joint activation of all EVs   0 = not selected .     .                             1 = selected .     .                             Bit4: EV rear .     .                             Bit6: EV front .     .                             Bit8-15: Intensity in 1% per Bit .     .                                      00 = off .     .                                      01 - FF = on ---------------------------------------------------------------- 002A  Joint activation of all AVs   0 = not selected .     .                             1 = selected .     .                             Bit5: AV rear .     .                             Bit7: AV front .     .                             Bit8-15: Intensity in 1% per Bit .     .                                      00 = off .     .                                      01 - FF = on ---------------------------------------------------------------- 0030  EV front (EV-V)               0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 0032  AV front (AV-V)               0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 0038  EV rear (EV-H)                0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 003A  AV rear (AV-H)                0000: off .     .                             0001-FFF: on .     .                             Resolution: 1% per Bit ---------------------------------------------------------------- 005E  Disable Valve-Protection      A5: disable shut down .     .                             00: enable shut down ---------------------------------------------------------------- 0064  Disable VR-shut down          A5: disable shut down .     .                             00: enable shut down ---------------------------------------------------------------- 0068  Disable abort of diagnosis    FF: disable shut down .     by speed limit                00: enable abort  Note: The AVs are used as a switch valve. When the activation value is not 0%, the software set it to 100% automatically |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dynamic-test"></a>
### STATUS_DYNAMIC_TEST

Read status DynamicTest KWP2000:      $33 RequestRoutineResultsByLocalId $05 DynamicTest Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DELTA_V_FRONT_VALUE | real | Delta v (wheel speed) front 0..337km/h |
| STAT_DELTA_V_REAR_VALUE | real | Delta v (wheel speed) rear 0..337km/h |
| STAT_DELTA_V_UNIT | string | km/h |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wss-front-missing-teeth-test"></a>
### STEUERN_WSS_FRONT_MISSING_TEETH_TEST

Activating front missing teeth test KWP2000: $30 InputOutputControlByLocalId $06 Front missing teeth test $07 InputOutputControlParameter Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wss-front-missing-teeth-test"></a>
### STATUS_WSS_FRONT_MISSING_TEETH_TEST

Status Missing teeth test KWP2000:      $33 RequestRoutingResultsByLocalId $06 WSSFrontMissingTeethTest Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WSS_MISS_TEETH_TEXT | string | table Status_WSS_Miss_Teeth |
| STAT_WSS_MISS_TEETH_VALUE | unsigned char | table Status_WSS_Miss_Teeth |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wss-rear-missing-teeth-test"></a>
### STEUERN_WSS_REAR_MISSING_TEETH_TEST

Activating rear missing teeth test KWP2000: $30 InputOutputControlByLocalId $06 Rear missing teeth test $07 InputOutputControlParameter Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wss-rear-missing-teeth-test"></a>
### STATUS_WSS_REAR_MISSING_TEETH_TEST

Status Missing teeth test KWP2000:      $33 RequestRoutingResultsByLocalId $07 WSSRearMissingTeethTest Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WSS_MISS_TEETH_TEXT | string | table Status_WSS_Miss_Teeth |
| STAT_WSS_MISS_TEETH_VALUE | unsigned char | table Status_WSS_Miss_Teeth |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stop-actuation"></a>
### STEUERN_STOP_ACTUATION

KWP2000: $30 InputOutputControlByLocalId $10 Local ID StopActuation $07 InputOutputControlParameter Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-return-pump"></a>
### STEUERN_RETURN_PUMP

Activating the return pump KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-all-valves"></a>
### STEUERN_ALL_VALVES

Activating all valves KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-front"></a>
### STEUERN_EV_FRONT

Activating EV front KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | int | Bereich: 0 bis 100 [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-rear"></a>
### STEUERN_EV_REAR

Activating EV rear KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | int | Bereich: 0 bis 100 [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-av-front"></a>
### STEUERN_AV_FRONT

Activating AV front KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-av-rear"></a>
### STEUERN_AV_REAR

Activating AV rear KWP2000: $30 InputOutputControlByLocalId $04 Local ID actuator test $07 InputOutputControlParameter Implementation see Appendix B: Acutator Table Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-telegramm-test"></a>
### _STEUERN_TELEGRAMM_TEST

Activating of the acutator test KWP2000: $30 InputOutputControlByLocalId $XX $07 InputOutputControlParameter Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA_STRING | binary |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-variant"></a>
### STATUS_VARIANT

Lesen der angelernten Variante KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FZG_CODE_NR | int | Fahrzeugcodierung table Variante_Datensatz |
| STAT_FZG_CODE_TEXT | string | Fahrzeugvaraiante table Variante_Datensatz |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-input"></a>
### STATUS_DIGITAL_INPUT

Read digital input signals KWP2000: $21 ReadDataByLocalIdentifier $03 digital input Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VALVE_RELAY | int | Valve relay status |
| STAT_ABS_SAFETY_LAMP | int | ABS safety lamp 1 =&gt; Lamp OFF 2 =&gt; Indication with 1Hz 4 =&gt; Indication with 4Hz 5 =&gt; Lamp ON 7 =&gt; Signal is invalid |
| STAT_ABS_SAFETY_LAMP_TEXT | string | ABS safety lamp text |
| STAT_ABS_OFF_SWITCH | int | ABS OFF switch status |
| STAT_EV | int | Inlet valve front |
| STAT_AV | int | Outlet valve front |
| STAT_EH | int | Inlet valve rear |
| STAT_AH | int | Outlet valve rear |
| STAT_RETURN_PUMP | int | Return pump |
| STAT_BRAKE_LIGHT_SWITCH_FRONT | int | Front BLS 0 =&gt; Switch not activated 1 =&gt; Switch activated 4 =&gt; Switch error 7 =&gt; Signal is invalid |
| STAT_BRAKE_LIGHT_SWITCH_FRONT_TEXT | string | FrontBrakeLightSwitch text |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-steuern-variante-k15"></a>
### STEUERN_VARIANTE_K15

Codierung Variante K15 KWP2000: $2E   WriteDataByCommonIdentifier $3000 CodingDataSet

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FZG_CODE | unsigned char | Fahrzeugvaraiante table Variante_Datensatz Werte: 	0x01 K15 HE - Hardenduro 0x02 K15 SM - Supermoto 0x03 K15 SC - Scrambler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-variante-r13"></a>
### STEUERN_VARIANTE_R13

Codierung Variante R13 KWP2000: $2E   WriteDataByCommonIdentifier $3000 CodingDataSet

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FZG_CODE | unsigned char | Fahrzeugvaraiante table Variante_Datensatz Werte: 	0x04 R13/31 0x05 R13/40 Basis 0x06 R13/40 Enduro |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (118 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (21 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (10 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [DIGITAL_2](#table-digital-2) (1 × 9)
- [DIGITAL_1](#table-digital-1) (1 × 4)
- [BLS_STATUS](#table-bls-status) (5 × 2)
- [STATUS_EVACFILL_AND_REPAIRBLEEDING](#table-status-evacfill-and-repairbleeding) (7 × 2)
- [STATUS_WSS_MISS_TEETH](#table-status-wss-miss-teeth) (4 × 2)
- [VARIANTE_DATENSATZ](#table-variante-datensatz) (8 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 5 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x10 | D-CAN |
| 0x0F | BMW-FAST |
| 0x0D | KWP2000* |
| 0x0C | KWP2000 |
| 0x06 | DS2 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 95 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED__SECURITY_ACCESS_REQUESTED |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0x41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0x42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0x43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0x51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0x52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0x53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0x72 | ERROR_ECU_TRANSFER_ABORTED |
| 0x74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0x75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0x76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0x77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIAGNOSTIC_MODE |
| ?00? | OKAY |
| ?02? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?03? | ERROR_ECU_INCORRECT_LEN |
| ?04? | ERROR_ECU_INCORRECT_LIN_RESPONSE_ID |
| ?05? | ERROR_ECU_INCORRECT_LIN_LEN |
| ?10? | ERROR_F_CODE |
| ?11? | ERROR_TABLE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
| ?41? | ERROR_BAUDRATE |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_DATA_OUT_OF_RANGE |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| ?73? | ERROR_NO_BIN_BUFFER |
| ?74? | ERROR_BIN_BUFFER |
| ?75? | ERROR_DATA_TYPE |
| ?76? | ERROR_CHECKSUM |
| ?80? | ERROR_FLASH_SIGNATURE_CHECK |
| ?81? | ERROR_VEHICLE_IDENTIFICATION_NR |
| ?82? | ERROR_PROGRAMMING_DATE |
| ?83? | ERROR_ASSEMBLY_NR |
| ?84? | ERROR_CALIBRATION_DATASET_NR |
| ?85? | ERROR_EXHAUST_REGULATION_OR_TYPE_APPROVAL_NR |
| ?86? | ERROR_REPAIR_SHOP_NR |
| ?87? | ERROR_TESTER_SERIAL_NR |
| ?88? | ERROR_MILAGE |
| ?89? | ERROR_PROGRAMMING_REFERENCE |
| ?8A? | ERROR_NO_FREE_UIF |
| ?8B? | ERROR_MAX_UIF |
| ?8C? | ERROR_SIZE_UIF |
| ?8D? | ERROR_LEVEL |
| ?8E? | ERROR_KEY |
| ?8F? | ERROR_AUTHENTICATION |
| ?90? | ERROR_NO_DREF |
| ?91? | ERROR_CHECK_PECUHN |
| ?92? | ERROR_CHECK_PRGREF |
| ?93? | ERROR_AIF_NR |
| ?94? | ERROR_CHECK_DREF |
| ?95? | ERROR_CHECK_HWREF |
| ?96? | ERROR_CHECK_HWREF |
| ?97? | ERROR_CHECK_PRGREFB |
| ?98? | ERROR_CHECK_VMECUH*NB |
| ?99? | ERROR_CHECK_PRGREFB |
| ?9A? | ERROR_CHECK_VMECUH*N |
| ?9B? | ERROR_MOST_CAN_GATEWAY_DISABLE |
| ?9C? | ERROR_NO_P2MIN |
| ?9D? | ERROR_NO_P2MAX |
| ?9E? | ERROR_NO_P3MIN |
| ?9F? | ERROR_NO_P3MAX |
| ?A0? | ERROR_NO_P4MIN |
| ?B0? | ERROR_DIAG_PROT |
| ?B1? | ERROR_SG_ADRESSE |
| ?B2? | ERROR_SG_MAXANZAHL_AIF |
| ?B3? | ERROR_SG_GROESSE_AIF |
| ?B4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?B5? | ERROR_SG_AUTHENTISIERUNG |
| ?C0? | ERROR_TELEGRAM_LEN_OUT_OFF_RANGE |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 118 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Continental Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO =&gt; BERU |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
| 0x72 | AISIN AW CO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | AKsys GmbH |
| 0x86 | META System |
| 0x87 | Hülsbeck & Fürst GmbH & Co KG |
| 0x88 | Mann & Hummel Automotive GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.A. |
| 0x92 | CRH |
| 0x93 | TPO Display Corp. |
| 0x94 | KÜSTER Automotive Control |
| 0x95 | Hitachi Automotive |
| 0x96 | Continental Automotive |
| 0x97 | TI-Automotive |
| 0x98 | Hydro |
| 0x99 | Johnson Controls |
| 0x9A | Takata- Petri |
| 0x9B | Mitsubishi Electric B.V. (Melco) |
| 0x9C | Autokabel |
| 0x9D | GKN-Driveline |
| 0x9E | Zollner Elektronik AG |
| 0x9F | PEIKER acustics GmbH |
| 0xA0 | Bosal-Oris |
| 0xA1 | Cobasys |
| 0xA2 | Lighting Reutlingen GmbH |
| 0xA3 | CONTI VDO |
| 0xA4 | ADC Automotive Distance Control Systems GmbH |
| 0xA5 | Funkwerk Dabendorf GmbH |
| 0xA6 | Lame |
| 0xA7 | Magna/Closures |
| 0xA8 | Wanyu |
| 0xA9 | Thyssen Krupp Presta |
| 0xAA | ArvinMeritor |
| 0xAB | Kongsberg Automotive GmbH |
| 0xFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
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

<a id="table-authentisierung"></a>
### AUTHENTISIERUNG

Dimensions: 4 rows × 2 columns

| AUTH_NR | AUTH_TEXT |
| --- | --- |
| 0x01 | Simple |
| 0x02 | Symetrisch |
| 0x03 | Asymetrisch |
| 0xFF | Keine |

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 14 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x81 | DEFAULT | DefaultMode |
| 0x82 | PT | PeriodicTransmissions |
| 0x84 | EOLSSM | EndOfLineSystemSupplierMode |
| 0x85 | ECUPM | ECUProgrammingMode |
| 0x86 | ECUDM | ECUDevelopmentMode |
| 0x87 | ECUAM | ECUAdjustmentMode |
| 0x88 | ECUVCM | ECUVariantCodingMode |
| 0x89 | ECUSM | ECUSafetyMode |
| 0xFA | SSS_A | SystemSupplierSpecific (A) |
| 0xFB | SSS_B | SystemSupplierSpecific (B) |
| 0xFC | SSS_C | SystemSupplierSpecific (C) |
| 0xFD | SSS_D | SystemSupplierSpecific (D) |
| 0xFE | SSS_E | SystemSupplierSpecific (E) |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-baudrate"></a>
### BAUDRATE

Dimensions: 7 rows × 3 columns

| NR | BAUD | BAUD_TEXT |
| --- | --- | --- |
| 0x01 | PC9600 | Baudrate 9.6 kBaud |
| 0x02 | PC19200 | Baudrate 19.2 kBaud |
| 0x03 | PC38400 | Baudrate 38.4 kBaud |
| 0x04 | PC57600 | Baudrate 57.6 kBaud |
| 0x05 | PC115200 | Baudrate 115.2 kBaud |
| 0x06 | SB | Specific Baudrate |
| 0xXY | -- | unbekannte Baudrate |

<a id="table-speichersegment"></a>
### SPEICHERSEGMENT

Dimensions: 12 rows × 3 columns

| SEG_BYTE | SEG_NAME | SEG_TEXT |
| --- | --- | --- |
| 0x00 | LAR | linearAdressRange |
| 0x01 | ROMI | ROM / EPROM, internal |
| 0x02 | ROMX | ROM / EPROM, external |
| 0x03 | NVRAM | NV-RAM (characteristic zones, DTC memory |
| 0x04 | RAMIS | RAM, internal (short MOV) |
| 0x05 | RAMXX | RAM, external (x data MOV) |
| 0x06 | FLASH | Flash EPROM, internal |
| 0x07 | UIFM | User Info Field Memory |
| 0x08 | VODM | Vehicle Order Data Memory |
| 0x09 | FLASHX | Flash EPROM, external |
| 0x0B | RAMIL | RAM, internal (long MOV / Register) |
| 0xFF | ??? | unbekanntes Speichersegment |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 21 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x6322 | Impulsgeber vorn, Signal: fehlt  |
| 0x6324 | Impulsgeber vorn, Signal: unplausibel |
| 0x6325 | Impulsgeber vorn, Luftspalt |
| 0x633E | Impulsgeber hinten, Signal: fehlt |
| 0x6340 | Impulsgeber hinten, Signal: unplausibel |
| 0x6341 | Impulsgeber hinten, Luftspalt |
| 0x6350 | Ventil Übertemperaturschutz |
| 0x635C | Radschlupf |
| 0x635E | Impulsgeber Spannungsversorgung, Kurzschluss nach + |
| 0x638C | Pumpenmotor |
| 0x6390 | Ventilrelais |
| 0x6398 | Einlassventil vorn |
| 0x639D | Auslassventil vorn |
| 0x63B3 | Einlassventil hinten |
| 0x63B8 | Auslassventil hinten |
| 0x63BC | Bordnetz Ueberspannung |
| 0x63BD | Bordnetz Unterspannung |
| 0x63C0 | Variantenkodierung: fehlerhaft |
| 0x63C1 | Steuergerät: interner Fehler |
| 0x63C2 | ABS Taster |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | DIGITAL_1 | DIGITAL_2 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x02 | Geschwindigkeit | km/h | - | unsigned char | - | 2 | 1 | 0 |
| 0x06 | ABS aktiv | 0/1 | - | 0x01 | - | 1 | 1 | 0 |
| 0x07 | ABS OFF Funktion aktiv | 0/1 | - | 0x02 | - | 1 | 1 | 0 |
| 0x08 | BLS vorne | 0/1 | - | 0x04 | - | 1 | 1 | 0 |
| 0x09 | BLS hinten | 0/1 | - | 0x08 | - | 1 | 1 | 0 |
| 0x0A | EV vorne | 0/1 | - | 0x10 | - | 1 | 1 | 0 |
| 0x0B | EV hinten | 0/1 | - | 0x20 | - | 1 | 1 | 0 |
| 0x0C | AV vorne | 0/1 | - | 0x40 | - | 1 | 1 | 0 |
| 0x0D | AV hinten | 0/1 | - | 0x80 | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-digital-2"></a>
### DIGITAL_2

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D |

<a id="table-digital-1"></a>
### DIGITAL_1

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x03 | 0x04 | 0x05 |

<a id="table-bls-status"></a>
### BLS_STATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Schalter aktiv |
| 0x02 | Schalter nicht aktiv |
| 0x04 | Fehler Schalter |
| 0x07 | Signal ungültig |
| 0xXY | ungültig |

<a id="table-status-evacfill-and-repairbleeding"></a>
### STATUS_EVACFILL_AND_REPAIRBLEEDING

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Funktion wurde initialisiert |
| 0x01 | Funktion noch nicht beendet |
| 0x02 | Funktion beendet |
| 0x04 | Funktion wurde unterbrochen |
| 0x08 | Fehler während Funktion |
| 0x10 | Initialisierung während Funktion |
| 0xXY | ungültig |

<a id="table-status-wss-miss-teeth"></a>
### STATUS_WSS_MISS_TEETH

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Ergebnis nicht möglich |
| 0x02 | Ergebnis erfolgreich |
| 0x03 | Ergebnis fehlerhaft |
| 0xXY | ungültig |

<a id="table-variante-datensatz"></a>
### VARIANTE_DATENSATZ

Dimensions: 8 rows × 2 columns

| VAR_NR | VAR_TEXT |
| --- | --- |
| 0x00 | keine Variante codiert |
| 0x01 | K15 HE - Hardenduro |
| 0x02 | K15 SM - Supermoto |
| 0x03 | K15 SC - Scrambler |
| 0x04 | R13/31 |
| 0x05 | R13/40 Basis |
| 0x06 | R13/40 Enduro |
| 0xXY | ungültig |
