# dsm_72.prg

- Jobs: [21](#jobs)
- Tables: [28](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Direct Select Module (Parksperrensteuergerät) |
| ORIGIN | BMW EA_514 Blass |
| REVISION | 2.103 |
| AUTHOR | ESG_GmbH EA-514 Palm, TietoEnator AMS Wegener, TietoEnator AMS  |
| COMMENT | N/A |
| PACKAGE | 1.07 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [STEUERN_IO](#job-steuern-io) - Vorgeben eines Status UDS  : $2F InputOutputControlByIdentifier
- [STEUERN_ROUTINE](#job-steuern-routine) - Vorgeben eines Status UDS  : $31 RoutineControl
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [_CHECK_ECU_LIVES](#job-check-ecu-lives) - Sends a telegramm and checks for an answer
- [_TEL_ROH](#job-tel-roh) - Ausführen eines Telegramms nur mit Übergabe der Daten ignoriert Leerzeichen Format 001122 ....
- [STATUS_DSM_PARKPOSITION](#job-status-dsm-parkposition) - StatusDSMParkPositiondaten UDS  : $22   ReadDataByIdentifier UDS  : $3F31 Sub-Parameter SGBD-Index Modus: Default
- [STATUS_DSM_NOTPFAD](#job-status-dsm-notpfad) - StausDSMNotpfaddaten UDS  : $22   ReadDataByIdentifier UDS  : $3F33 Sub-Parameter SGBD-Index Modus: Default
- [STATUS_DSM](#job-status-dsm) - StausDSMdaten UDS  : $22   ReadDataByIdentifier UDS  : $3F35 Sub-Parameter SGBD-Index Modus: Default
- [STATUS_DSM_FASTA](#job-status-dsm-fasta) - StausDSMFasta UDS  : $22   ReadDataByIdentifier UDS  : $3F37 Sub-Parameter SGBD-Index Modus: Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $06 reportDTCExtendedDataRecordByDTCNumber Modus: Default
- [IDENT](#job-ident) - Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $3F30 Sub-Parameter SGBD-Index Modus: Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob Modus   : Default

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

<a id="job-check-ecu-lives"></a>
### _CHECK_ECU_LIVES

Sends a telegramm and checks for an answer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-tel-roh"></a>
### _TEL_ROH

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

<a id="job-status-dsm-parkposition"></a>
### STATUS_DSM_PARKPOSITION

StatusDSMParkPositiondaten UDS  : $22   ReadDataByIdentifier UDS  : $3F31 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DSM_POSITION_SOLL_TEXT | string | "P" entspr. HCP fordert Position "P" "R" entspr. HCP fordert Position "R" "N" entspr. HCP fordert Position "N" "D" entspr. HCP fordert Position "D" "IDLE" entspr. HCP fordert Position "IDLE" "SNA" entspr. HCP hat sendet keine oder ungültige Parkposition (Signal Not Available) table POSITION_SOLL_NR TEXT |
| STAT_DSM_POSITION_SOLL_NR | int | "8" entspr. HCP fordert Position "P" "7" entspr. HCP fordert Position "R" "6" entspr. HCP fordert Position "N" "5" entspr. HCP fordert Position "D" "0" entspr. HCP fordert Position "IDLE" "15" entspr. HCP hat sendet keine oder ungültige Parkposition (Signal Not Available) table POSITION_SOLL_NR NR |
| STAT_DSM_POSITION_IST_TEXT | string | "P" entspr. DSM in Position "P" "P-R" entspr. DSM zwischen Position "P" und "R" "R" entspr. DSM in Position "R" "R-N" entspr. DSM zwischen Position "R" und "N" "N" entspr. DSM in Position "N" "N-D" entspr. DSM zwischen Position "N" und "D" "D" entspr. DSM in Position "D" "SNA" entspr. DSM kann Position nicht ermitteln (Signal Not Available) table POSITION_IST_NR TEXT |
| STAT_DSM_POSITION_IST_NR | int | "8" entspr. DSM in Position "P" "13" entspr. DSM zwischen Position "P" und "R" "7" entspr. DSM in Position "R" "12" entspr. DSM zwischen Position "R" und "N" "6" entspr. DSM in Position "N" "11" entspr. DSM zwischen Position "N" und "D" "5" entspr. DSM in Position "D" "15" entspr. DSM kann Position nicht ermitteln (Signal Not Available) table POSITION_IST_NR NR |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |

<a id="job-status-dsm-notpfad"></a>
### STATUS_DSM_NOTPFAD

StausDSMNotpfaddaten UDS  : $22   ReadDataByIdentifier UDS  : $3F33 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DSM_ZUSTAND_NOTSYSTEM_AUSGELOEST | int | "1" entspr. Notpfad hat ausgelöst/Feder ist entspannt "0" entspr. Notpfad nicht ausgelöst/Normalbetrieb table ZUSTAND_NOTSYSTEM_AUSGELOEST NR |
| STAT_DSM_NOTPFAD_NOTPFAD_FREIGEGEBEN | int | "1" entspr. Notpfad freigegeben/ Notsystem kann ausgelöst werden "0" entspr. Notpfad gesperrt/ Notsystem kann nicht auslösen table NOTPFAD_NOTPFAD_FREIGEGEBEN NR |
| STAT_DSM_ZAEHLER_NOTSYSTEM_WERT | int | "x" entspr. Anzahl der Auslösevorgänge |
| STAT_DSM_ZAEHLER_NOTSYSTEM_EINH | string | dummy to avoid compiling error |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |

<a id="job-status-dsm"></a>
### STATUS_DSM

StausDSMdaten UDS  : $22   ReadDataByIdentifier UDS  : $3F35 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DSM_KL30_SPANNUNG_WERT | real | "x" entspr. Spannung an DSM KL30 |
| STAT_DSM_KL30_SPANNUNG_EINH | string | "V" entspr. Volt |
| STAT_DSM_TEMPERATUR_WERT | real | "x" entspr. Temperatur im DSM |
| STAT_DSM_TEMPERATUR_EINH | string | "°C" entspr. Grad Celsius |
| STAT_DSM_AUXMOTOR_SPANNUNG_WERT | real | "x" entspr. Spannung am AUX-Eingang DSM |
| STAT_DSM_AUXMOTOR_SPANNUNG_EINH | string | "V" entspr. Volt |
| STAT_DSM_POSITION_WINKEL_WERT | real | "x" entspr. Winkelposition der Rasterscheibe |
| STAT_DSM_POSITION_WINKEL_EINH | string | "°" entspr. Grad |
| STAT_DSM_SERVICEQUALIFIER_TEXT | string | "Init" "Power Latch" "Limphome temporary emergency" "Test Mode" "Limphome permanent emergency" "Normalbetrieb" "P in Emergency" "Limphome Aux-Motor" "SNA" table SERVICEQUALIFIER_NR TEXT |
| STAT_DSM_SERVICEQUALIFIER_NR | int | "13" für "Init" "8" für "Power Latch" "9" für "Limphome temporary emergency" "12" für "Testmode" "11" für "Limphome permanent emergency" "1" für "Normalbetrieb" "2" für "P in Emergency" "3" für Limphome Aux-Motor "15" für SNA table SERVICEQUALIFIER_NR NR |
| STAT_DSM_ANGELERNT | int | "1" entspr. DSM ist angelernt "0" entspr. DSM ist nicht angelernt bzw. Lernwert verloren |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |

<a id="job-status-dsm-fasta"></a>
### STATUS_DSM_FASTA

StausDSMFasta UDS  : $22   ReadDataByIdentifier UDS  : $3F37 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DSM_COUNTER_NOTLAUF_1 | long | "x" entspr. Anzahl Notläufe Plausibel |
| STAT_DSM_COUNTER_NOTLAUF_2 | long | "x" entspr. Anzahl Notläufe Blind |
| STAT_DSM_TEMPERATURVERTEILUNG_MINUS50_BIS_MINUS41 | long | "temperaturstatistik -50C bis -41C" |
| STAT_DSM_TEMPERATURVERTEILUNG_MINUS40_BIS_MINUS31 | long | "temperaturstatistik -40C bis -31C" |
| STAT_DSM_TEMPERATURVERTEILUNG_MINUS30_BIS_MINUS21 | long | "temperaturstatistik -30C bis -21C" |
| STAT_DSM_TEMPERATURVERTEILUNG_MINUS20_BIS_MINUS11 | long | "temperaturstatistik -20C bis -11C" |
| STAT_DSM_TEMPERATURVERTEILUNG_MINUS10_BIS_MINUS1 | long | "temperaturstatistik -10C bis -1C" |
| STAT_DSM_TEMPERATURVERTEILUNG_0_BIS_9 | long | "temperaturstatistik 0C bis 9C" |
| STAT_DSM_TEMPERATURVERTEILUNG_10_BIS_19 | long | "temperaturstatistik 10C bis 19C" |
| STAT_DSM_TEMPERATURVERTEILUNG_20_BIS_29 | long | "temperaturstatistik 20C bis 29C" |
| STAT_DSM_TEMPERATURVERTEILUNG_30_BIS_39 | long | "temperaturstatistik 30C bis 39C" |
| STAT_DSM_TEMPERATURVERTEILUNG_40_BIS_49 | long | "temperaturstatistik 40C bis 49C" |
| STAT_DSM_TEMPERATURVERTEILUNG_50_BIS_59 | long | "temperaturstatistik 50C bis 59C" |
| STAT_DSM_TEMPERATURVERTEILUNG_60_BIS_69 | long | "temperaturstatistik 60C bis 69C" |
| STAT_DSM_TEMPERATURVERTEILUNG_70_BIS_79 | long | "temperaturstatistik 70C bis 79C" |
| STAT_DSM_TEMPERATURVERTEILUNG_80_BIS_89 | long | "temperaturstatistik 80C bis 89C" |
| STAT_DSM_TEMPERATURVERTEILUNG_90_BIS_99 | long | "temperaturstatistik 90C bis 99C" |
| STAT_DSM_TEMPERATURVERTEILUNG_100_BIS_109 | long | "temperaturstatistik 100C bis 109C" |
| STAT_DSM_TEMPERATURVERTEILUNG_110_BIS_119 | long | "temperaturstatistik 110C bis 119C" |
| STAT_DSM_TEMPERATURVERTEILUNG_120_BIS_129 | long | "temperaturstatistik 120C bis 129C" |
| STAT_DSM_TEMPERATURVERTEILUNG_130_BIS_139 | long | "temperaturstatistik 130C bis 139C" |
| STAT_DSM_TEMPERATURVERTEILUNG_140_BIS_149 | long | "temperaturstatistik 140C bis 149C" |
| STAT_DSM_TEMPERATURVERTEILUNG_MIN | long | "Minimum Temperatur" |
| STAT_DSM_TEMPERATURVERTEILUNG_MAX | long | "Maximum Temperatur" |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |

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

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $06 reportDTCExtendedDataRecordByDTCNumber Modus: Default

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
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text |
| F_UW_KM | long | Umweltbedingung Kilometerstand (3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_KM_START | unsigned int | Kilometerstand beim ersten Auftreten |
| F_KM_LETZTES | unsigned int | Kilometerstand beim letzten Auftreten |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| F_SAE_CODE | unsigned int | Wertebereich 0x000000 - 0xFFFFFF externe Tabelle T_SCOD |
| F_SAE_CODE_STRING | string | 5 stelliger Text in der Form 'Sxxxx' |
| F_SAE_CODE_TEXT | string | Text zu F_SAE_CODE |
| _RESPONSE_SNAPSHOT | binary | Hex-Antwort von SG |
| _RESPONSE_EXTENDED_DATA | binary | Hex-Antwort von SG |
| _RESPONSE_SEVERITY | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident"></a>
### IDENT

Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $3F30 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardware-Versionsindex (= Hardware Version Number Byte #3) |
| ID_COD_INDEX | int | Codier-Index Dummy-Wert |
| ID_DIAG_INDEX | long | Index zur Erkennung der SG-Variante Hybrid Generation 1.0 liefert nur 2 Antwort-Byte |
| ID_VAR_INDEX | int | Varianten-Index Dummy-Wert |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) Dummy-Wert |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten buffer_2 |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) Dummy-Wert |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) Dummy-Wert |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-Auftrag an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |
| _REQUEST4 | binary | Hex-Auftrag an SG |
| _RESPONSE4 | binary | Hex-Antwort von SG |
| _REQUEST5 | binary | Hex-Auftrag an SG |
| _RESPONSE5 | binary | Hex-Antwort von SG |
| _REQUEST6 | binary | Hex-Auftrag an SG |
| _RESPONSE6 | binary | Hex-Antwort von SG |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | string | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | unsigned int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZAHL_PROG | unsigned int | Anzahl Programmiervorgaenge |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |
| _REQUEST04 | binary | Hex-Auftrag an SG |
| _RESPONSE04 | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (64 × 2)
- [LIEFERANTEN](#table-lieferanten) (111 × 2)
- [FARTTEXTE](#table-farttexte) (18 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (24 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (9 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (4 × 16)
- [ARG_0X1000](#table-arg-0x1000) (1 × 12)
- [TAB_POSITION](#table-tab-position) (9 × 2)
- [RES_0X1000](#table-res-0x1000) (1 × 10)
- [TAB_MODUS](#table-tab-modus) (2 × 2)
- [ARG_0X2011](#table-arg-0x2011) (1 × 14)
- [HYBRID_LIEF](#table-hybrid-lief) (6 × 2)
- [DATUM_MONAT](#table-datum-monat) (53 × 2)
- [POSITION_SOLL_NR](#table-position-soll-nr) (6 × 2)
- [POSITION_IST_NR](#table-position-ist-nr) (8 × 2)
- [SERVICEQUALIFIER_NR](#table-servicequalifier-nr) (9 × 2)
- [FORTTEXTE](#table-forttexte) (53 × 3)
- [FORTUMWELTNR](#table-fortumweltnr) (52 × 6)

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

Dimensions: 111 rows × 2 columns

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

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 4 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VERSTELLEN | 0x2011 | - | Drive to position P, R, N or D | - | - | - | - | - | - | - | - | 0x95 | 31 | ARG_0x2011 | - |
| STEUERGERAETEMODUS | 0x1000 | - | Switch Device Mode | - | - | - | - | - | - | - | - | 0x95 | 2F | ARG_0x1000 | RES_0x1000 |
| LADENDSMRUECKFALLSYSTEM | 0x2012 | - | Load whole P in emergency concept | - | - | - | - | - | - | - | - | 0x95 | 31 | - | - |
| ANLERNEN | 0x2019 | - | Learning of drive positions | - | - | - | - | - | - | - | - | 0x95 | 31 | - | - |

<a id="table-arg-0x1000"></a>
### ARG_0X1000

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERGERAETEMODUS | - | - | char | - | TAB_MODUS | - | - | - | 0 | 2 | - |

<a id="table-tab-position"></a>
### TAB_POSITION

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | P |
| 0x01 | R |
| 0x02 | N |
| 0x03 | D |
| 0x10 | P slow |
| 0x11 | R slow |
| 0x12 | N slow |
| 0x13 | D slow |
| 0x23 | 3° before D |

<a id="table-res-0x1000"></a>
### RES_0X1000

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_DSM_MODUS_NR | 0-n | - | char | - | TAB_MODUS | - | - | - | - |

<a id="table-tab-modus"></a>
### TAB_MODUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x02 | Testmodus |
| 0x01 | Slavemode |

<a id="table-arg-0x2011"></a>
### ARG_0X2011

Dimensions: 1 rows × 14 columns

| ARG | STR | STPR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POSITION | + | - | - | - | char | - | TAB_POSITION | - | - | - | 0 | 100 | - |

<a id="table-hybrid-lief"></a>
### HYBRID_LIEF

Dimensions: 6 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0003 | Bosch |
| 0040 | Delphi |
| 007E | Hitachi |
| 009C | Cobasys |
| 0008 | Siemens |
| FFFF | undefinierter Lieferant |

<a id="table-datum-monat"></a>
### DATUM_MONAT

Dimensions: 53 rows × 2 columns

| KW | MON |
| --- | --- |
| 0x01 | 0x01 |
| 0x02 | 0x01 |
| 0x03 | 0x01 |
| 0x04 | 0x01 |
| 0x05 | 0x01 |
| 0x06 | 0x02 |
| 0x07 | 0x02 |
| 0x08 | 0x02 |
| 0x09 | 0x02 |
| 0x0A | 0x03 |
| 0x0B | 0x03 |
| 0x0C | 0x03 |
| 0x0D | 0x03 |
| 0x0E | 0x04 |
| 0x0F | 0x04 |
| 0x10 | 0x04 |
| 0x11 | 0x04 |
| 0x12 | 0x04 |
| 0x13 | 0x05 |
| 0x14 | 0x05 |
| 0x15 | 0x05 |
| 0x16 | 0x05 |
| 0x17 | 0x06 |
| 0x18 | 0x06 |
| 0x19 | 0x06 |
| 0x1A | 0x06 |
| 0x1B | 0x07 |
| 0x1C | 0x07 |
| 0x1D | 0x07 |
| 0x1E | 0x07 |
| 0x1F | 0x07 |
| 0x20 | 0x08 |
| 0x21 | 0x08 |
| 0x22 | 0x08 |
| 0x23 | 0x08 |
| 0x24 | 0x09 |
| 0x25 | 0x09 |
| 0x26 | 0x09 |
| 0x27 | 0x09 |
| 0x28 | 0x0A |
| 0x29 | 0x0A |
| 0x2A | 0x0A |
| 0x2B | 0x0A |
| 0x2C | 0x0A |
| 0x2D | 0x0B |
| 0x2E | 0x0B |
| 0x2F | 0x0B |
| 0x30 | 0x0B |
| 0x31 | 0x0C |
| 0x32 | 0x0C |
| 0x33 | 0x0C |
| 0x34 | 0x0C |
| 0xFF | 0x00 |

<a id="table-position-soll-nr"></a>
### POSITION_SOLL_NR

Dimensions: 6 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | HCP fordert Position IDLE |
| 0x05 | HCP fordert Position D |
| 0x06 | HCP fordert Position N |
| 0x07 | HCP fordert Position R |
| 0x08 | HCP fordert Position P |
| 0x0f | HCP hat sendet keine oder ungültige Parkposition (Signal not available) |

<a id="table-position-ist-nr"></a>
### POSITION_IST_NR

Dimensions: 8 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x05 | DSM in Position D |
| 0x06 | DSM in Position N |
| 0x07 | DSM in Position R |
| 0x08 | DSM in Position P |
| 0x0b | DSM zwischen Position N und D |
| 0x0c | DSM zwischen Position R und N |
| 0x0d | DSM zwischen Position P und R |
| 0x0f | DSM kann Position nicht ermitteln (Signal not available) |

<a id="table-servicequalifier-nr"></a>
### SERVICEQUALIFIER_NR

Dimensions: 9 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x01 | Normalbetrieb |
| 0x02 | P in Emergency |
| 0x03 | Limphome Aux-Motor |
| 0x08 | Power Latch |
| 0x09 | Limphome temporary emergency |
| 0x0b | Limphome permanent emergency |
| 0x0c | Testmode |
| 0x0d | Init |
| 0x0f | SNA (Signal not available) |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 53 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x440000 | DSM:  Leitungsfehler.  KL30 Unterspannung | 0 |
| 0x440001 | DSM:  Leitungsfehler.  KL30 Überspannung | 0 |
| 0x440002 | DSM:  Leitungsfehler.  AUX Versorgung Kurzschluss nach Plus oder Dauer-Bestromung durch HCP | 0 |
| 0x440010 | DSM: interner Fehler. Laufzeit-Fehler | 0 |
| 0x440011 | DSM: interner Fehler. Testroutine fehlerhaft | 0 |
| 0x440012 | DSM: interner Fehler. Leichter EEPROM Fehler | 0 |
| 0x440013 | DSM: interner Fehler. Unerwartete Prozessor Anweisung | 0 |
| 0x440019 | DSM: interner Fehler. Schwerer EEPROM Fehler | 0 |
| 0x440014 | DSM: interner Fehler. RAM Check | 0 |
| 0x440015 | DSM: interner Fehler. ROM Check | 0 |
| 0x440016 | DSM: interner Fehler. Frequenz- oder Pulsweiten-Modulation fehlerhaft | 0 |
| 0x440017 | DSM: interner Fehler. Positionssensor fehlerhaft | 0 |
| 0x440018 | DSM: interner Fehler. Bauteil H-Brücke Hauptmotor fehlerhaft | 0 |
| 0x440020 | DSM: interner Fehler. Abgleichwerte fehlen | 0 |
| 0x440021 | DSM: interner Fehler. AUX Motor Sensor | 0 |
| 0x440022 | DSM: interner Fehler. Bauteil H-Brücke Hilfsmotor fehlerhaft | 0 |
| 0x440030 | DSM: Sollposition unerreichbar. Fehler Motorfunktion oder Parksperre | 0 |
| 0x440031 | DSM: Sollposition unerreichbar. Fehler Notmotor oder Rückstellfeder | 0 |
| 0x440032 | DSM: Sollposition unerreichbar. Fehler AUX Motor Rückstellung | 0 |
| 0x440033 | DSM: Sollposition unerreichbar. Rückfallebene deaktiviert. Fehlerfallzähler größer 100 | 0 |
| 0x440034 | DSM: Sollposition unerreichbar. Kalibrierung/ Einlernroutine fehlerhaft durchgeführt | 0 |
| 0x440040 | DSM: Ereignisfehler. Ersatzsystem ausgelöst | 0 |
| 0x440041 | DSM: Ereignisfehler. Programmierbedingungen unerfüllt | 0 |
| 0x440042 | DSM: Ereignisfehler. Eigenständiges P-Einlegen infolge fehlender Information des HCP | 0 |
| 0x440043 | DSM: Ereignisfehler. DSM Ruhestromfehler | 0 |
| 0x440044 | DSM: Ereignisfehler. EWS unerlaubterweise aktiv | 0 |
| 0x440045 | DSM: Ereignisfehler. Kalibrierung verloren oder Einlernroutine nicht durchgeführt | 0 |
| 0x440046 | DSM: Ereignisfehler. Unterspannung während Verstellung Parksperre | 0 |
| 0x440047 | DSM: Ereignisfehler. Unterspannung während Spannen der Rückstellfeder | 0 |
| 0xEE4400 | DSM: HL-CAN: Kommunikationsfehler | 0 |
| 0xEE5401 | Botschaft (Daten HCP,  0x300) fehlt, Empfänger DSM, Sender HCP | 0 |
| 0xEE5402 | Botschaft (Daten HCP, 0x300) nicht aktuell, Empfänger DSM, Sender HCP | 0 |
| 0xEE5403 | Botschaft (Daten HCP, 0x300) Prüfsumme falsch, Empfänger DSM, Sender HCP | 0 |
| 0xEE5404 | Botschaft (Radgeschwindigkeit Hybrid, 0xB2) fehlt, Empfänger DSM, Sender HIM | 0 |
| 0xEE5405 | Botschaft (ETEI Hybrid General Status 1, 0xB4) fehlt, Empfänger DSM, Sender HCP | 0 |
| 0xEE5406 | Botschaft (Klemmenstatus Hybrid, 0x130) fehlt, Empfänger DSM, Sender HIM | 0 |
| 0xEE5407 | Botschaft (Klemmenstatus Hybrid, 0x130) nicht aktuell, Empfänger DSM, Sender HIM | 0 |
| 0xEE5408 | Botschaft (Klemmenstatus Hybrid, 0x130) Prüfsumme falsch, Empfänger DSM, Sender HIM | 0 |
| 0xEE5409 | Botschaft (PPEI_Vehicle_Speed_and_Distance, 0x3E9) fehlt, Empfänger DSM, Sender DME | 0 |
| 0xEE5410 | Botschaft (KOMBI_39Fh, 0x39F) fehlt, Empfänger DSM, Sender HIM | 0 |
| 0xEE5411 | Botschaft (HGM100, 0x396) fehlt, Empfänger DSM, Sender HIM | 0 |
| 0xEE6C00 | Schnittstelle HCP (SL_POSN_RQ, 0x300): Signal ungültig | 0 |
| 0xEE6C01 | Schnittstelle HIM (KM_KI, 0x396): Signal ungültig | 0 |
| 0xEE6C02 | Schnittstelle HIM (ST_KL_15_HYB, 0x130): Signal ungültig | 0 |
| 0xEE6C03 | Schnittstelle HIM (DAT_ZEIT_JAHR, 0x39F): Signal ungültig | 0 |
| 0xEE6C04 | Schnittstelle HIM (DAT_ZEIT_MONAT,  0x39F): Signal ungültig | 0 |
| 0xEE6C05 | Schnittstelle HIM (DAT_ZEIT_TAG, 0x39F): Signal ungültig | 0 |
| 0xEE6C06 | Schnittstelle HIM (V_WHL_RRH_HYB, 0xB2): Signal ungültig | 0 |
| 0xEE6C07 | Schnittstelle HIM (V_WHL_RLH_HYB, 0xB2): Signal ungültig | 0 |
| 0xEE6C08 | Schnittstelle HIM (V_WHL_FRH_HYB, 0xB2): Signal ungültig | 0 |
| 0xEE6C09 | Schnittstelle HIM (V_WHL_FLH_HYB, 0xB2): Signal ungültig | 0 |
| 0xEE6C10 | Schnittstelle DME (VehSpdAvgNDrvnV, 0x3E9): Signal ungültig | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fortumweltnr"></a>
### FORTUMWELTNR

Dimensions: 52 rows × 6 columns

| ORT | F_UW1_NR | F_UW2_NR | F_UW3_NR | F_UW4_NR | F_UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 0x440000 |  |  |  |  |  |
| 0x440001 |  |  |  |  |  |
| 0x440002 |  |  |  |  |  |
| 0x440010 |  |  |  |  |  |
| 0x440011 |  |  |  |  |  |
| 0x440012 | 58 | 59 | 20 | 21 | 22 |
| 0x440013 |  |  |  |  |  |
| 0x440019 | 58 | 59 | 20 | 21 | 22 |
| 0x440014 |  |  |  |  |  |
| 0x440015 |  |  |  |  |  |
| 0x440016 |  |  |  |  |  |
| 0x440017 | 54 | 55 | 56 | 57 |  |
| 0x440018 | 9 | 10 | 11 | 12 |  |
| 0x440020 |  |  |  |  |  |
| 0x440021 |  |  |  |  |  |
| 0x440022 | 9 | 10 | 11 | 12 |  |
| 0x440030 | 31 | 52 | 53 | 60 |  |
| 0x440031 | 31 |  |  |  |  |
| 0x440032 | 31 |  |  |  |  |
| 0x440033 |  |  |  |  |  |
| 0x440034 | 31 |  |  |  |  |
| 0x440040 | 41 |  |  |  |  |
| 0x440041 |  |  |  |  |  |
| 0x440042 | 37 | 38 |  |  |  |
| 0x440043 |  |  |  |  |  |
| 0x440044 | 44 | 45 |  |  |  |
| 0x440045 |  |  |  |  |  |
| 0x440046 |  |  |  |  |  |
| 0x440047 |  |  |  |  |  |
| 0xEE4400 |  |  |  |  |  |
| 0xEE5401 |  |  |  |  |  |
| 0xEE5402 |  |  |  |  |  |
| 0xEE5403 |  |  |  |  |  |
| 0xEE5404 |  |  |  |  |  |
| 0xEE5405 |  |  |  |  |  |
| 0xEE5406 |  |  |  |  |  |
| 0xEE5407 |  |  |  |  |  |
| 0xEE5408 |  |  |  |  |  |
| 0xEE5409 |  |  |  |  |  |
| 0xEE5410 |  |  |  |  |  |
| 0xEE5411 |  |  |  |  |  |
| 0xEE6C00 |  |  |  |  |  |
| 0xEE6C01 |  |  |  |  |  |
| 0xEE6C02 |  |  |  |  |  |
| 0xEE6C03 |  |  |  |  |  |
| 0xEE6C04 |  |  |  |  |  |
| 0xEE6C05 |  |  |  |  |  |
| 0xEE6C06 | 28 | 29 | 30 |  |  |
| 0xEE6C07 | 27 | 29 | 30 |  |  |
| 0xEE6C08 | 27 | 28 | 29 |  |  |
| 0xEE6C09 | 27 | 28 | 30 |  |  |
| 0xEE6C10 |  |  |  |  |  |
