# Dsc_87_EF73.prg

- Jobs: [65](#jobs)
- Tables: [20](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Dynamische Stabilitaets Control DSC E87,E90 |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 0.02 |
| AUTHOR | BMW EF-73 Kusch |
| COMMENT | Conti_Teves MK60, BMW_FAST, E8x,E9x ausser E83/84 |
| PACKAGE | 1.17 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_AEI_LESEN](#job-c-aei-lesen) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - Starten eines Diagnose-Modus KWP2000:$10,$87 StartDiagnosticSession
- [SEED](#job-seed) - Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service
- [FS_LOESCHEN](#job-fs-loeschen) - KWP2000: $14 ClearDiagnosticInformation Fehlerspeicher loeschen Job DIAGNOSE_MODE ist integriert
- [IDENT_PRODUCTION_DATA](#job-ident-production-data) - KWP2000: $1A,$8F ReadECUIdentification Ident-Daten des SG ...
- [IDENT_VIN](#job-ident-vin) - KWP2000: $1A,$90 ReadECUIdentification Ident-Daten des SG ...
- [IDENT_TEVES_ECU_SW_NR](#job-ident-teves-ecu-sw-nr) - KWP2000: $1A,$94 ReadECUIdentification Ident-Daten des SG ...
- [IDENT_PROGRAMMING_DATE](#job-ident-programming-date) - KWP2000: $1A,$99 ReadECUIdentification Ident-Daten des SG ...
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Diag_Mode ist integriert KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default
- [C_AEI_SCHREIBEN](#job-c-aei-schreiben) - Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_AUFTRAG](#job-c-aei-auftrag) - Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $3000 Codierdaten lesen Modus    : Default
- [COD_SCHREIBEN](#job-cod-schreiben) - KWP2000: $2E WriteDataByCommonIdentifier $3000 Codierdaten schreiben Es muessen 14 Codierdaten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 14 die CS wird automatisch berechnet Die Checksumme im ersten Datenbyte wird automatisch berechnet Job DIAGNOSE_MODE ist integriert
- [STATUS_RADGESCHWINDIGKEIT](#job-status-radgeschwindigkeit) - KWP2000: $21,$07 ReadDataByLocalIdentifier service Radgeschwindigkeiten auslesen
- [STATUS_SCHALTER](#job-status-schalter) - KWP2000: $21,$05 ReadDataByLocalIdentifier service
- [STATUS_SENSOREN](#job-status-sensoren) - KWP2000: $21,$06 ReadDataByLocalIdentifier service
- [STATUS_SENSOREN_OFFSET](#job-status-sensoren-offset) - KWP2000: $21,$02 ReadDataByLocalIdentifier service
- [DRUCKSENSOR_DSC_ABGLEICHEN](#job-drucksensor-dsc-abgleichen) - KWP2000: $31,$20 StartRoutineByLocalIdentifier service
- [LENKWINKEL_DSC_ABGLEICHEN](#job-lenkwinkel-dsc-abgleichen) - KWP2000: $31,$21 StartRoutineByLocalIdentifier service
- [QUERBESCHLEUNIGUNG_DSC_ABGLEICHEN](#job-querbeschleunigung-dsc-abgleichen) - KWP2000: $31,$22 StartRoutineByLocalIdentifier service
- [BET_AKTIV](#job-bet-aktiv) - Bandendetest aktivieren KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_AKTIV beinhaltet den Job DIAGNOSE_MODE
- [BET_PASSIV](#job-bet-passiv) - Bandendetest passiv schalten KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_PASSIV beinhaltet den Job DIAGNOSE_MODE
- [STEUERN_DIGITAL](#job-steuern-digital) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2
- [STEUERN_DIGITAL_WARNLAMPEN](#job-steuern-digital-warnlampen) - KWP2000:$30,$20,$07 InputOutputControlByLocalIdentifier service Ansteuerung Warnlampen ueber CAN Parameterliste: E or W,
- [STEUERN_DIGITAL_BLS](#job-steuern-digital-bls) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 BLS
- [STEUERN_DIGITAL_SEQ](#job-steuern-digital-seq) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) 
- [STEUERN_ANALOG_CAN_MSR](#job-steuern-analog-can-msr) - KWP2000: $30,$30,$07 InputOutputControlByLocalIdentifier service Ansteuern MSR ueber CAN Parameterliste: E or W,MD_MSR (0 ...100)%
- [STEUERN_ANALOG_CAN_ASC_LM](#job-steuern-analog-can-asc-lm) - KWP2000: $30,$30,$07 InputOutputControlByLocalIdentifier service Ansteuern MSR ueber CAN Parameterliste: E or W,MD_ASC (0 ...100)%, MD_LM (0 ...100)%
- [NA_ENTLUEFTUNG_RE](#job-na-entlueftung-re) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [NA_ENTLUEFTUNG_LI](#job-na-entlueftung-li) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [VAKUUM](#job-vakuum) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [VAKUUM_PUMPE](#job-vakuum-pumpe) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [IDENT_SCHREIBEN](#job-ident-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $80 BMW Identifikation schreiben
- [IDENT_PROGRAMMING_DATE_SCHREIBEN](#job-ident-programming-date-schreiben) - KWP2000:$3B,$99 WriteDataByLocalIdentifier service Ident-Daten des SG schreiben
- [IDENT_PRODUCTION_DATA_SCHREIBEN](#job-ident-production-data-schreiben) - KWP2000:$3B,$8F WriteDataByLocalIdentifier service Ident-Daten des SG schreiben
- [STATUS_CAN_DME_1_LESEN](#job-status-can-dme-1-lesen) - Auslesen der CAN Botschaft DME_1 KWP2000: $22 ReadDataByCommonIdentifier $0316 CAN_DDE_1 Modus    : Default
- [STATUS_CAN_DME_2_LESEN](#job-status-can-dme-2-lesen) - Auslesen der CAN Botschaft DME_2 KWP2000: $22 ReadDataByCommonIdentifier $0329 CAN_DME_2 Modus    : Default
- [STATUS_CAN_DDE_3_LESEN](#job-status-can-dde-3-lesen) - Auslesen der CAN Botschaft DDE_3 KWP2000: $22 ReadDataByCommonIdentifier $0235 CAN_DDE_3 Modus    : Default
- [STATUS_CAN_LWS_1_LESEN](#job-status-can-lws-1-lesen) - Auslesen der CAN Botschaft LWS_1 KWP2000: $22 ReadDataByCommonIdentifier $01F5 CAN_LWS_1 Modus    : Default
- [STATUS_LWS_LI_RE_MAX](#job-status-lws-li-re-max) - Auslesen der CAN Botschaft LWS_1 KWP2000: $22 ReadDataByCommonIdentifier $01F5 CAN_LWS_1 Job laeuft max. 16 sec: werden die Max-Werte vorher erreicht, wird der Job abgebrochen
- [STATUS_CAN_EGS_1_LESEN](#job-status-can-egs-1-lesen) - Auslesen der CAN Botschaft EGS_1 KWP2000: $22 ReadDataByCommonIdentifier $043F CAN_EGS_1 Modus    : Default
- [STATUS_LESEN_RPA](#job-status-lesen-rpa) - KWP2000:$21,$04 ReadDataByLocalIdentifier service
- [RPA_RESET](#job-rpa-reset) - KWP2000:$31,$25 StartRoutineByLocalIdentifier service
- [RPA_EOL_PASSIV](#job-rpa-eol-passiv) - KWP2000:$31,$26 StartRoutineByLocalIdentifier service
- [FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus    : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt !) Musterparametersatz: ROMI,0xFF12AB,12,Datenbytes Argumente mit "Strich_Punkt" getrennt (nicht mit Komma !) 0x04,0x05,0x0B,0x0C...Datenbytes(hex) durch Komma getrennt !) 04,05,03,11,12 ... Datenbytes(dec) durch Komma getrennt !) das High-Byte ist bei R.Bosch DSC_60 immer 0xFFxxxx KWP2000: $3D WriteMemoryByAddress Modus  : Default

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

<a id="job-ident"></a>
### IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
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
| ID_SG_ADR | long | Steuergeraeteadresse |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-normaler-datenverkehr"></a>
### NORMALER_DATENVERKEHR

Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREIGEBEN | string | "ja"   -&gt; normalen Datenverkehr freigeben "nein" -&gt; normalen Datenverkehr sperren table DigitalArgument TEXT |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-ci-lesen"></a>
### C_CI_LESEN

Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_COD_INDEX | int | Codier-Index |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen"></a>
### C_AEI_LESEN

Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

Starten eines Diagnose-Modus KWP2000:$10,$87 StartDiagnosticSession

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-seed"></a>
### SEED

Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MODE_TEXT | string | Mode als Textausgabe |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, oder FEHLER |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

KWP2000: $14 ClearDiagnosticInformation Fehlerspeicher loeschen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-production-data"></a>
### IDENT_PRODUCTION_DATA

KWP2000: $1A,$8F ReadECUIdentification Ident-Daten des SG ...

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vin"></a>
### IDENT_VIN

KWP2000: $1A,$90 ReadECUIdentification Ident-Daten des SG ...

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer 14-stellig, WBA vorangestellt |
| FG_NR_MINI | string | Fahrgestellnummer 14-stellig, WMW vorangestellt |
| FG_NR_7 | string | Fahrgestellnummer 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-teves-ecu-sw-nr"></a>
### IDENT_TEVES_ECU_SW_NR

KWP2000: $1A,$94 ReadECUIdentification Ident-Daten des SG ...

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_NR | string | Softwarenummer 12 Zeichen |
| SW_DATUM | string | Herstelldatum (TT.MM.JJ) |
| SW_ZEIT | string | Uhrzeit (STD:MIN) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-programming-date"></a>
### IDENT_PROGRAMMING_DATE

KWP2000: $1A,$99 ReadECUIdentification Ident-Daten des SG ...

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Diag_Mode ist integriert KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

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
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) Es muss 1 String mit 18 Zeichen uebergeben werden das letzte Zeichen ist ein Dummy z.B. WBAAX71010JR250001 FG_NR: WBAAX71010JR25000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG, schreiben |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag ans SG, lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG, schreiben |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG, lesen |

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) Es muss 1 String mit 18 Zeichen uebergeben werden das letzte Zeichen ist ein Dummy z.B. WBAAX71010JR250001 FG_NR: WBAAX71010JR25000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben"></a>
### C_AEI_SCHREIBEN

Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag"></a>
### C_AEI_AUFTRAG

Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG, schreiben |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag ans SG, lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG, schreiben |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG, lesen |

<a id="job-c-c-schreiben"></a>
### C_C_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $3000 Codierdaten lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cod-schreiben"></a>
### COD_SCHREIBEN

KWP2000: $2E WriteDataByCommonIdentifier $3000 Codierdaten schreiben Es muessen 14 Codierdaten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 14 die CS wird automatisch berechnet Die Checksumme im ersten Datenbyte wird automatisch berechnet Job DIAGNOSE_MODE ist integriert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_BYTES | string | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radgeschwindigkeit"></a>
### STATUS_RADGESCHWINDIGKEIT

KWP2000: $21,$07 ReadDataByLocalIdentifier service Radgeschwindigkeiten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-schalter"></a>
### STATUS_SCHALTER

KWP2000: $21,$05 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_HANDBREMSE_SCHALTER_EIN | int | 0 oder 1 |
| STAT_DSC_TASTER_EIN | int | 0 oder 1 |
| STAT_BREMSFLUESSIGKEIT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_RPA_RESET_TASTER_EIN | int | 0 oder 1 |
| STAT_RPA_EOL_PASSIV | int | 0 oder 1 |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensoren"></a>
### STATUS_SENSOREN

KWP2000: $21,$06 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DREHRATENSENSOR_GESCHW_WERT | real | Geschwindigkeitswert des Drehratensensor [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_WERT | real | Beschleunigungswert des Querbeschleunigungssensor [g] |
| STAT_DRUCKSENSOR_DRUCKSTANGENKREIS_DRUCK_WERT | real | Druckwert des Druckstangenkreissensors [bar] |
| STAT_DRUCKSENSOR_SCHWIMMKREIS_DRUCK_WERT | real | Druckwert des Druckstangenkreissensors [bar] |
| STAT_SENSOR_TEMPERATUR_WERT | real | Temperatur im Steuergeraet [Grad] |
| STAT_SPANNUNG_UREF_WERT | real | Spannung [Volt] |
| STAT_SPANNUNG_PUMPE_WERT | real | Spannung [Volt] |
| STAT_SPANNUNG_KLEMME_30_WERT | real | Spannung [Volt] |
| STAT_SPANNUNG_VCC_WERT | real | Spannung [Volt] |
| STAT_SENSOR_TEMPERATUR_EINH | string | [Grad] |
| STAT_DREHRATENSENSOR_GESCHW_EINH | string | [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNGSSENSOR_EINH | string | [g] |
| STAT_SENSOR_DRUCK_EINH | string | bar |
| STAT_SENSOR_SPANNUNG_EINH | string | Volt |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensoren-offset"></a>
### STATUS_SENSOREN_OFFSET

KWP2000: $21,$02 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_OFFSET_LENKWINKEL_WERT | real | Offsetwert des Lenkwinkels |
| STAT_OFFSET_LENKWINKEL_EINH | string | Einheit des Offsetwerts des Lenkwinkels [Grad] |
| STAT_OFFSET_QUERBESCHLEUNIGUNG_WERT | real | Offsetwert der Querbeschleunigung |
| STAT_OFFSET_QUERBESCHLEUNIGUNG_EINH | string | Einheit des Offsetwerts der Querbeschleunigung [g] |
| STAT_OFFSET_DREHRATE_WERT | real | Offsetwert der Drehrate |
| STAT_OFFSET_DREHRATE_EINH | string | Einheit des Offsetwertes der Drehrate [Grad/sec] |
| STAT_OFFSET_DRUCKSENSOR_1_WERT | real | Offsetwert des Lenkwinkels |
| STAT_OFFSET_DRUCKSENSOR_1_EINH | string | Einheit des Offsetwerts des Drucksensors 1 [bar] |
| STAT_OFFSET_DRUCKSENSOR_2_WERT | real | Offsetwert des Lenkwinkels |
| STAT_OFFSET_DRUCKSENSOR_2_EINH | string | Einheit des Offsetwerts des Drucksensors 2 [bar] |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-drucksensor-dsc-abgleichen"></a>
### DRUCKSENSOR_DSC_ABGLEICHEN

KWP2000: $31,$20 StartRoutineByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lenkwinkel-dsc-abgleichen"></a>
### LENKWINKEL_DSC_ABGLEICHEN

KWP2000: $31,$21 StartRoutineByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-querbeschleunigung-dsc-abgleichen"></a>
### QUERBESCHLEUNIGUNG_DSC_ABGLEICHEN

KWP2000: $31,$22 StartRoutineByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bet-aktiv"></a>
### BET_AKTIV

Bandendetest aktivieren KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_AKTIV beinhaltet den Job DIAGNOSE_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bet-passiv"></a>
### BET_PASSIV

Bandendetest passiv schalten KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_PASSIV beinhaltet den Job DIAGNOSE_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-digital-warnlampen"></a>
### STEUERN_DIGITAL_WARNLAMPEN

KWP2000:$30,$20,$07 InputOutputControlByLocalIdentifier service Ansteuerung Warnlampen ueber CAN Parameterliste: E or W,

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-digital-bls"></a>
### STEUERN_DIGITAL_BLS

KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 BLS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-digital-seq"></a>
### STEUERN_DIGITAL_SEQ

KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| S1 | string | gewuenschte Komponente 1 |
| S2 | string | gewuenschte Komponente 2 |
| S3 | string | gewuenschte Komponente 3 |
| S4 | string | gewuenschte Komponente 4 |
| S5 | string | gewuenschte Komponente 5 |
| S6 | string | gewuenschte Komponente 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-analog-can-msr"></a>
### STEUERN_ANALOG_CAN_MSR

KWP2000: $30,$30,$07 InputOutputControlByLocalIdentifier service Ansteuern MSR ueber CAN Parameterliste: E or W,MD_MSR (0 ...100)%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| MD_MSR | int | gewuenschter wert in % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-analog-can-asc-lm"></a>
### STEUERN_ANALOG_CAN_ASC_LM

KWP2000: $30,$30,$07 InputOutputControlByLocalIdentifier service Ansteuern MSR ueber CAN Parameterliste: E or W,MD_ASC (0 ...100)%, MD_LM (0 ...100)%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| MD_ASC | int | gewuenschter wert in % |
| MD_LM | int | gewuenschter wert in % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-na-entlueftung-re"></a>
### NA_ENTLUEFTUNG_RE

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-na-entlueftung-li"></a>
### NA_ENTLUEFTUNG_LI

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-vakuum"></a>
### VAKUUM

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-vakuum-pumpe"></a>
### VAKUUM_PUMPE

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-ident-schreiben"></a>
### IDENT_SCHREIBEN

KWP2000: $3B WriteDataByLocalIdentifier $80 BMW Identifikation schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 29 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 29 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-programming-date-schreiben"></a>
### IDENT_PROGRAMMING_DATE_SCHREIBEN

KWP2000:$3B,$99 WriteDataByLocalIdentifier service Ident-Daten des SG schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 4 Ident_Daten als ein Hex_String uebergeben werden: z.B. 19,99,12,27 Datum: 27.12.1999 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-production-data-schreiben"></a>
### IDENT_PRODUCTION_DATA_SCHREIBEN

KWP2000:$3B,$8F WriteDataByLocalIdentifier service Ident-Daten des SG schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 12 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,02,03,04,05 ... 12 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-dme-1-lesen"></a>
### STATUS_CAN_DME_1_LESEN

Auslesen der CAN Botschaft DME_1 KWP2000: $22 ReadDataByCommonIdentifier $0316 CAN_DDE_1 Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORDREHZAHL_WERT | real | Motordrehzahl [U/Min] |
| STAT_MOTORDREHZAHL_EINH | string | [U/Min] |
| STAT_MD_IND_NE_WERT | real | indiziertes Motormoment nach Momenteneingriff [% von MD-Norm] |
| STAT_MD_IND_NE_EINH | string | [% von MD_NORM] |
| STAT_MD_IND_WERT | real | indiziertes Motormoment [% von MD-Norm] |
| STAT_MD_IND_EINH | string | [% von MD_NORM] |
| STAT_MD_REIB_WERT | real | Reibmoment des Motors [% von MD-Norm] |
| STAT_MD_REIB_EINH | string | [% von MD_NORM] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-dme-2-lesen"></a>
### STATUS_CAN_DME_2_LESEN

Auslesen der CAN Botschaft DME_2 KWP2000: $22 ReadDataByCommonIdentifier $0329 CAN_DME_2 Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-dde-3-lesen"></a>
### STATUS_CAN_DDE_3_LESEN

Auslesen der CAN Botschaft DDE_3 KWP2000: $22 ReadDataByCommonIdentifier $0235 CAN_DDE_3 Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-lws-1-lesen"></a>
### STATUS_CAN_LWS_1_LESEN

Auslesen der CAN Botschaft LWS_1 KWP2000: $22 ReadDataByCommonIdentifier $01F5 CAN_LWS_1 Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKWINKEL_WERT | real | Einschlag Lenkrad [Grad] |
| STAT_LENKWINKEL_EINH | string | [Grad] |
| STAT_LENKWINKEL_GESCHW_WERT | real | Geschwindigkeit Lenkeinschlag [Grad/sec] |
| STAT_LENKWINKEL_GESCHW_EINH | string | [Grad/sec] |
| STAT_ID_LWS | int | Identifikation LWS Sensor |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lws-li-re-max"></a>
### STATUS_LWS_LI_RE_MAX

Auslesen der CAN Botschaft LWS_1 KWP2000: $22 ReadDataByCommonIdentifier $01F5 CAN_LWS_1 Job laeuft max. 16 sec: werden die Max-Werte vorher erreicht, wird der Job abgebrochen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKWINKEL_WERT_LI_MAX | real | Einschlag Lenkrad [Grad] |
| STAT_LENKWINKEL_WERT_RE_MAX | real | Einschlag Lenkrad [Grad] |
| STAT_LENKWINKEL_WERT_LI_MAX_SAR | real | Einschlag Lenkrad/10 [Grad] fuer SAR Pruefstand |
| STAT_LENKWINKEL_WERT_RE_MAX_SAR | real | Einschlag Lenkrad/10 [Grad] fuer SAR Pruefstand |
| STAT_LENKWINKEL_EINH | string | [Grad] |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-egs-1-lesen"></a>
### STATUS_CAN_EGS_1_LESEN

Auslesen der CAN Botschaft EGS_1 KWP2000: $22 ReadDataByCommonIdentifier $043F CAN_EGS_1 Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-rpa"></a>
### STATUS_LESEN_RPA

KWP2000:$21,$04 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STATUS_KM_RESET | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STATUS_KM_WARNUNG | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STATUS_KM_RESET_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STATUS_KM_WARNUNG_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STATUS_KM_RESET_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| STATUS_KM_WARNUNG_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| DRUCKSCHWELLE_GROB_15_70_KMH | int |  |
| DRUCKSCHWELLE_GROB_70_110_KMH | int |  |
| DRUCKSCHWELLE_GROB_110_150_KMH | int |  |
| DRUCKSCHWELLE_GROB_150_190_KMH | int |  |
| DRUCKSCHWELLE_GROB_190_220_KMH | int |  |
| DRUCKSCHWELLE_GROB_220_250_KMH | int |  |
| DRUCKSCHWELLE_FEIN_15_70_KMH | int |  |
| DRUCKSCHWELLE_FEIN_70_110_KMH | int |  |
| DRUCKSCHWELLE_FEIN_110_150_KMH | int |  |
| DRUCKSCHWELLE_FEIN_150_190_KMH | int |  |
| DRUCKSCHWELLE_FEIN_190_220_KMH | int |  |
| DRUCKSCHWELLE_FEIN_220_250_KMH | int |  |
| MOMENTENKOMPENSATION_1 | int |  |
| MOMENTENKOMPENSATION_2 | int |  |
| MOMENTENKOMPENSATION_3 | int |  |
| MOMENTENKOMPENSATION_4 | int |  |
| MOMENTENKOMPENSATION_5 | int |  |
| MOMENTENKOMPENSATION_6 | int |  |
| KURVENKOMPENSATION_LINKS_50_PROZ | int |  |
| KURVENKOMPENSATION_LINKS_100_PROZ | int |  |
| KURVENKOMPENSATION_RECHTS_50_PROZ | int |  |
| KURVENKOMPENSATION_RECHTS_100_PROZ | int |  |
| WARNUNG_AKTUELL | int |  |
| LERNZAEHLERSTAND | int |  |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-rpa-reset"></a>
### RPA_RESET

KWP2000:$31,$25 StartRoutineByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-rpa-eol-passiv"></a>
### RPA_EOL_PASSIV

KWP2000:$31,$26 StartRoutineByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-fs-lesen-sar"></a>
### FS_LESEN_SAR

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt !) Musterparametersatz: ROMI,0xFF12AB,12,Datenbytes Argumente mit "Strich_Punkt" getrennt (nicht mit Komma !) 0x04,0x05,0x0B,0x0C...Datenbytes(hex) durch Komma getrennt !) 04,05,03,11,12 ... Datenbytes(dec) durch Komma getrennt !) das High-Byte ist bei R.Bosch DSC_60 immer 0xFFxxxx KWP2000: $3D WriteMemoryByAddress Modus  : Default

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (87 × 2)
- [LIEFERANTEN](#table-lieferanten) (63 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (77 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [DIGITAL1](#table-digital1) (1 × 5)
- [DIGITAL2](#table-digital2) (1 × 13)
- [FUMWELTTEXTE](#table-fumwelttexte) (17 × 9)
- [STEUERN](#table-steuern) (14 × 3)
- [WARNLAMPEN](#table-warnlampen) (8 × 3)
- [STEUERN_TEL](#table-steuern-tel) (14 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 87 rows × 2 columns

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
| ?81? | ERROR_VIHICLE_IDENTFICATON_NR |
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
| ?A0? | ERROR_DIAG_PROT |
| ?A1? | ERROR_SG_ADRESSE |
| ?A2? | ERROR_SG_MAXANZAHL_AIF |
| ?A3? | ERROR_SG_GROESSE_AIF |
| ?A4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?A5? | ERROR_SG_AUTHENTISIERUNG |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 63 rows × 2 columns

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
| 0x18 | Teves |
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
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
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

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Anlieferzustand |
| 0x01 | Normalbetrieb |
| 0x02 | nicht benutzt |
| 0x03 | Speicher geloescht |
| 0x04 | nicht benutzt |
| 0x05 | Signaturpruefung PAF nicht durchgefuehrt |
| 0x06 | Signaturpruefung DAF nicht durchgefuehrt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Hardwarereferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vorhanden oder nicht vollstaendig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vorhanden oder nicht vollstaendig |
| 0x10 | Reserviert fuer BMW |
| 0x80 | Reserviert fuer Zulieferer |
| 0xXY | unbekannter Programmierstatus |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 77 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D8C | Sensor-Cluster Timeout CAN |
| 0x5D8E | falscher Sensorcluster |
| 0x5D8F | Sensorcluster Fehler intern |
| 0x5D96 | Sensor-Cluster CAN Bus-Off |
| 0x5D97 | Sensorcluster Versorgungsspannung ausserhalb gueltigem Bereich |
| 0x5D99 | Sensor-Cluster CAN Fehler |
| 0x5D90 | Drehzahlfuehler vorne links elektrisch defekt |
| 0x5D91 | Drehzahlfuehler vorne links Extrapolation |
| 0x5D92 | Drehzahlfuehler Impulsrad vorne links periodische Ueberwachung |
| 0x5D93 | Drehzahlfuehler vorne links Anfahrerkennung v_Vergleich |
| 0x5D94 | Drehzahlfuehler vorne links Langzeitueberwachung |
| 0x5D95 | Drehzahlfuehler vorne links Check auf doppelte Impulsradfrequenz |
| 0x5DA0 | Drehzahlfuehler vorne rechts elektrisch defekt |
| 0x5DA1 | Drehzahlfuehler vorne rechts Extrapolation |
| 0x5DA2 | Drehzahlfuehler Impulsrad vorne rechts periodische Ueberwachung |
| 0x5DA3 | Drehzahlfuehler vorne rechts Anfahrerkennung v_Vergleich |
| 0x5DA4 | Drehzahlfuehler vorne rechts Langzeitueberwachung |
| 0x5DA5 | Drehzahlfuehler vorne rechts Check auf doppelte Impulsradfrequenz |
| 0x5DB0 | Drehzahlfuehler hinten links elektrisch defekt |
| 0x5DB1 | Drehzahlfuehler hinten links Extrapolation |
| 0x5DB2 | Drehzahlfuehler Impulsrad hinten links periodische Ueberwachung |
| 0x5DB3 | Drehzahlfuehler hinten links Anfahrerkennung v_Vergleich |
| 0x5DB4 | Drehzahlfuehler hinten links Langzeitueberwachung |
| 0x5DB5 | Drehzahlfuehler hinten links Check auf doppelte Impulsradfrequenz |
| 0x5DC0 | Drehzahlfuehler hinten rechts elektrisch defekt |
| 0x5DC1 | Drehzahlfuehler hinten rechts Extrapolation |
| 0x5DC2 | Drehzahlfuehler Impulsrad hinten rechts periodische Ueberwachung |
| 0x5DC3 | Drehzahlfuehler hinten rechts Anfahrerkennung v_Vergleich |
| 0x5DC4 | Drehzahlfuehler hinten rechts Langzeitueberwachung |
| 0x5DC5 | Drehzahlfuehler hinten rechts Check auf doppelte Impulsradfrequenz |
| 0x5DF0 | Pumpenmotor |
| 0x5DF2 | Ventil/ECU_Hardware Fehler,ROM/RAM_Check Fehler |
| 0x5DF4 | Bordnetzspannung &lt; 9 Volt |
| 0x5DF5 | Steuergeraet Fehler intern |
| 0x5DF7 | Bordnetzspannung &gt; 18 Volt |
| 0x5E00 | Bandendetest aktiv |
| 0x5E01 | Bandendetest Timeout |
| 0x5E02 | Bandendetest Gierraten Sensor Justierung Fehler |
| 0x5E03 | Bandendetest Gierraten Sensor Fehler |
| 0x5E04 | Bandendetest Querbeschleunigung Sensor Fehler |
| 0x5E05 | Bandendetest Querbeschleunigung und Gierraten Fehler |
| 0x5E06 | Bandendetest Gierraten Sensor falsch montiert |
| 0x5E07 | Bandendetest Querbeschleunigung und Gierraten Sensor falsch montiert |
| 0x5E08 | Bandendetest Lenkwinkel Sensor Fehler |
| 0x5E11 | CAN-Bus Off, Interner Fehler CAN-Controller |
| 0x5E14 | CAN Timeout DME/DDE |
| 0x5E15 | CAN Timeout EGS |
| 0x5E16 | CAN Timeout Instrumentenkombi |
| 0x5E18 | CAN DME/DDE Botschaft unplausibel |
| 0x5E19 | CAN DME/DDE, Motormoment nicht einstellbar |
| 0x5E1A | CAN DME/DDE Signal Fehler |
| 0x5E1E | CAN Timeout LWS |
| 0x5E1F | ABS/ASC/DSC: VIN nicht initialisiert, LWS-Abgleich durchfuehren |
| 0x5E20 | Druck Sensor 1 elektrisch defekt |
| 0x5E21 | Druck Sensor 2 elektrisch defekt |
| 0x5E24 | Druck Sensor 1/2 unplausibel |
| 0x5E26 | Spannungsversorgung Sensoren |
| 0x5E2F | Temperatur Sensor |
| 0x5E30 | Querbeschleunigung Sensor elektrisch defekt |
| 0x5E32 | Querbeschleunigung Sensor unplausibel |
| 0x5E38 | Gierraten Sensor elektrisch defekt |
| 0x5E3C | Gierraten Sensor unplausibel |
| 0x5E40 | Lenkwinkel Sensor Signal unplausibel,Offset |
| 0x5E43 | Lenkwinkel Sensor intern |
| 0x5E4E | DSC Sensor Offset Check |
| 0x5E4F | DSC Dauerregelung |
| 0x5E58 | ASC ECU empfaengt LWS CAN Botschaft |
| 0x5E59 | Codierfehler |
| 0x5E5B | DSC Taster laenger als 10sec gedrueckt oder Fehler |
| 0x5E5C | RPA Taster Fehler |
| 0x5E5D | Bremsfluessigkeitsniveau Schalter Fehler |
| 0x5E5E | Bremslichtschalter Fehler |
| 0x5DE0 | Bremsbelagverschleiss VA nicht/falsch initialisiert |
| 0x5DE1 | Bremsbelagverschleiss HA nicht/falsch initialisiert |
| 0x5DE2 | Bremsbelagverschleiss VA kritische Belagdicke erreicht |
| 0x5DE3 | Bremsbelagverschleiss HA kritische Belagdicke erreicht |
| 0xXY | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | DIGITAL1 | DIGITAL2 | - |

<a id="table-digital1"></a>
### DIGITAL1

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x02 | 0x03 | 0x04 | 0x05 |

<a id="table-digital2"></a>
### DIGITAL2

Dimensions: 1 rows × 13 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 12 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F | 0x10 | 0x11 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 17 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x02 | Bremslichtschalter | 0/1 | - | 0x01 | - | 1 | 1 | 0 |
| 0x03 | Bremsfluessigkeitsschalter | 0/1 | - | 0x04 | - | 1 | 1 | 0 |
| 0x04 | ASC/DSC_aktiv (Tasterfunktion) | 0/1 | - | 0x08 | - | 1 | 1 | 0 |
| 0x05 | Bremsdruck erkannt | 0/1 | - | 0x20 | - | 1 | 1 | 0 |
| 0x06 | ABS-Regelung | 0/1 | high | 0x0100 | - | 1 | 1 | 0 |
| 0x07 | ASC-Regelung (BMR) | 0/1 | high | 0x0200 | - | 1 | 1 | 0 |
| 0x08 | ASC-Regelung (AMR) | 0/1 | high | 0x0400 | - | 1 | 1 | 0 |
| 0x09 | GMR-Regelung (GMR) | 0/1 | high | 0x0800 | - | 1 | 1 | 0 |
| 0x0A | GMR-Regelung (MMR) | 0/1 | high | 0x1000 | - | 1 | 1 | 0 |
| 0x0B | CBC-Regelung | 0/1 | high | 0x2000 | - | 1 | 1 | 0 |
| 0x0C | MSR-Regelung | 0/1 | high | 0x4000 | - | 1 | 1 | 0 |
| 0x0D | TDR-Regelung  | 0/1 | high | 0x8000 | - | 1 | 1 | 0 |
| 0x0E | SDR-Regelung | 0/1 | high | 0x0001 | - | 1 | 1 | 0 |
| 0x0F | DBC-Regelung | 0/1 | high | 0x0002 | - | 1 | 1 | 0 |
| 0x10 | RTA aktiv | 0/1 | high | 0x0004 | - | 1 | 1 | 0 |
| 0x11 | Run-Up Mode | 0/1 | high | 0x0008 | - | 1 | 1 | 0 |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 14 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| EVVL | 0 | 0x01 |
| AVVL | 0 | 0x02 |
| EVVR | 0 | 0x04 |
| AVVR | 0 | 0x08 |
| EVHL | 0 | 0x10 |
| AVHL | 0 | 0x20 |
| EVHR | 0 | 0x40 |
| AVHR | 0 | 0x80 |
| SV1 | 1 | 0x01 |
| SV2 | 1 | 0x02 |
| EUV1 | 1 | 0x04 |
| EUV2 | 1 | 0x08 |
| PUMPE | 1 | 0x10 |
| XYZ | 1 | 0x00 |

<a id="table-warnlampen"></a>
### WARNLAMPEN

Dimensions: 8 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| ABS | 0 | 0x01 |
| DSC | 0 | 0x02 |
| BWL | 0 | 0x04 |
| HBA | 0 | 0x08 |
| L_ABS | 0 | 0x0E |
| L_DSC | 0 | 0x0D |
| L_BWL | 0 | 0x0B |
| L_HBA | 0 | 0x07 |

<a id="table-steuern-tel"></a>
### STEUERN_TEL

Dimensions: 14 rows × 2 columns

| TEL_NR | FRAME |
| --- | --- |
| S1 | 85,29,F1,30,10,07,00,1A |
| S2 | 85,29,F1,30,10,07,01,1A |
| S3 | 85,29,F1,30,10,07,00,15 |
| S4 | 85,29,F1,30,10,07,04,15 |
| S5 | 85,29,F1,30,10,07,54,1F |
| S6 | 85,29,F1,30,10,07,55,1F |
| S7 | 85,29,F1,30,10,07,52,1F |
| S8 | 85,29,F1,30,10,07,56,1F |
| S9 | 85,29,F1,30,10,07,45,1F |
| S10 | 85,29,F1,30,10,07,15,1F |
| S11 | 85,29,F1,30,10,07,50,0A |
| S12 | 85,29,F1,30,10,07,40,1A |
| S13 | 85,29,F1,30,10,07,10,1A |
| S14 | 85,29,F1,30,10,07,05,05 |
