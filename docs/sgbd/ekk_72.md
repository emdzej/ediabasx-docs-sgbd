# ekk_72.prg

- Jobs: [28](#jobs)
- Tables: [27](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EKK_72 |
| ORIGIN | BMW_Group EI-541_Mechatronik J.Falkenstein |
| REVISION | 3.000 |
| AUTHOR | DENSO ElectricThermalsystemR&D K.Tsutsui, BMW_Group EI-541_Mech |
| COMMENT | N/A |
| PACKAGE | 1.47 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [C_AEI_LESEN](#job-c-aei-lesen) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_SCHREIBEN](#job-c-aei-schreiben) - Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_AUFTRAG](#job-c-aei-auftrag) - Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [STATUS_EKK](#job-status-ekk) - Lesen EKK Status mit dem SGBD-Generator erzeugt
- [STEUERN_DREHZAHL](#job-steuern-drehzahl) - Ansteuern Drehzahl EKK KWP2000: $30 InputOutputControlByLocalIdentifier $01 Drehzahl $07 ShortTermAdjustment
- [_STAT_EKK_GW_SW](#job-stat-ekk-gw-sw) - Liest alle Status für EKK Entwicklerjob mit dem SGBD-Generator erzeugt
- [STEUERN_KURZSCHLUSS_UVW_EKK](#job-steuern-kurzschluss-uvw-ekk) - Ausfuehren IGBT_SHORT EKK KWP2000: $30 InputOutputControlByLocalIdentifier $02 IGBT_Short $07 ShortTermAdjustment

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

<a id="job-diagnoseprotokoll-lesen"></a>
### DIAGNOSEPROTOKOLL_LESEN

Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |
| DIAG_PROT_ANZAHL | int | Anzahl der Diagnoseprotokolle |
| DIAG_PROT_NR1 | string | Alle möglichen Diagnose-Protokolle Falls mehrere Protokolle möglich sind werden die entsprechenden Results DIAG_PROT_NRx dynamisch erzeugt |

<a id="job-diagnoseprotokoll-setzen"></a>
### DIAGNOSEPROTOKOLL_SETZEN

Wählt ein Diagnoseprotokoll aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_PROT | string | Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

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

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x0E) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x05) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen"></a>
### C_AEI_LESEN

Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben"></a>
### C_AEI_SCHREIBEN

Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag"></a>
### C_AEI_AUFTRAG

Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen"></a>
### SERIENNUMMER_LESEN

Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-physikalische-hw-nr-lesen"></a>
### PHYSIKALISCHE_HW_NR_LESEN

Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PHYSIKALISCHE_HW_NR | string | Physikalische Hardware-Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

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

<a id="job-status-ekk"></a>
### STATUS_EKK

Lesen EKK Status mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EKK_DREHZAHL_WERT | real | tbd Bereich von 0 [1/min] bis 8600 [1/min] |
| STAT_EKK_DREHZAHL_EINH | string | tbd Einheit: 1/min |
| STAT_EKK_HOCHVOLT_WERT | int | tbd table EKK_HOCHVOLT_Table WERT |
| STAT_EKK_HOCHVOLT_TEXT | string | tbd table EKK_HOCHVOLT_Table TEXT |
| STAT_EKK_UEBERLAST_WERT | int | tbd table EKK_UEBERLAST_Table WERT |
| STAT_EKK_UEBERLAST_TEXT | string | tbd table EKK_UEBERLAST_Table TEXT |
| STAT_EKK_KOMMUNIKATION_INTERN_WERT | int | tbd table EKK_KOMMUNIKATION_INTERN_Table WERT |
| STAT_EKK_KOMMUNIKATION_INTERN_TEXT | string | tbd table EKK_KOMMUNIKATION_INTERN_Table TEXT |
| STAT_EKK_STARTBEDINGUNG_WERT | int | tbd table EKK_STARTBEDINGUNG_Table WERT |
| STAT_EKK_STARTBEDINGUNG_TEXT | string | tbd table EKK_STARTBEDINGUNG_Table TEXT |
| STAT_EKK_STANDBY_JAMMING | int | 0=kein STB jamming, 1=STB jamming - Interne Überprüfung nicht erfolgreich! |
| STAT_EKK_STANDBY_SIGNAL | int | 0=STB signal AUS, 1=STB signal EIN |
| STAT_EKK_WECHSELRICHTER_UEBERHITZUNG_WERT | int | tbd table EKK_WECHSELRICHTER_UEBERHITZUNG_Table WERT |
| STAT_EKK_WECHSELRICHTER_UEBERHITZUNG_TEXT | string | tbd table EKK_WECHSELRICHTER_UEBERHITZUNG_Table TEXT |
| STAT_EKK_LEISTUNG_WERT | real | tbd Bereich von 0 [Watt] bis 12750 [Watt] |
| STAT_EKK_LEISTUNG_EINH | string | tbd Einheit: Watt |
| STAT_EKK_HV_STROM_WERT | real | tbd Bereich von 0 [Ampere] bis 25.4 [Ampere] |
| STAT_EKK_HV_STROM_EINH | string | tbd Einheit: Ampere |
| STAT_EKK_WECHSELRICHTER_TEMPERATUR_WERT | real | tbd Bereich von 0 [Grad] bis 127 [Grad] |
| STAT_EKK_WECHSELRICHTER_TEMPERATUR_EINH | string | tbd Einheit: Grad |
| STAT_EKK_HV_SPANNUNG_WERT | real | tbd Bereich von 100 [Volt] bis 608 [Volt] |
| STAT_EKK_HV_SPANNUNG_EINH | string | tbd Einheit: Volt |
| STAT_EKK_SPANNUNG_UBAT_WERT | real | tbd Bereich von 0 [Volt] bis 25.4 [Volt] |
| STAT_EKK_SPANNUNG_UBAT_EINH | string | tbd Einheit: Volt |
| STAT_EKK_LEISTUNGSBESCHRAENKUNG | int | 0=keine Leistungsbeschraenkung, 1=Leistungsbeschraenkung durch PEB |
| STAT_EKK_KURZSCHLUSS_UVW | int | 0=kein Kurzschluss_UVW, 1=Kurzschluss_UVW - IGBT-short wird durchgeführt! |
| STAT_EKK_SCHUTZABSCHALTUNG | int | 0=keine Schutzabschaltung, 1=Schutzabschaltung aktiv - Wird aufgehoben sobald der Fehler nicht mehr vorhanden! |
| STAT_EKK_SCHUTZABSCHALTUNG_HV_RESET | int | 0=keine Schutzabschaltung, 1=Schutzabschaltung aktiv - Hochspannung reset notwendig um Fehler zu beheben! |
| STAT_EKK_DREHZAHL_PROZENT_WERT | real | tbd Bereich von 0 [%] bis 100 [%] |
| STAT_EKK_DREHZAHL_PROZENT_EINH | string | tbd Einheit: % |
| STAT_EKK_KOMPRESSOR_BETRIEBSZUSTAND_WERT | int | tbd table CompStatus WERT |
| STAT_EKK_KOMPRESSOR_BETRIEBSZUSTAND_TEXT | string | tbd table CompStatus TEXT |
| STAT_EKK_SOLL_DREHZAHL_INTERN_WERT | real | tbd Bereich von 0 [1/min] bis 8600 [1/min] |
| STAT_EKK_SOLL_DREHZAHL_INTERN_EINH | string | tbd Einheit: 1/min |
| STAT_EKK_FREIGABE_INVERTER_INTERN | int | 0=STB AUS, 1=STB EIN |
| STAT_EKK_MOTOR_RUECKLESELEITUNG_WERT | int | tbd table EKK_MOTOR_RUECKLESELEITUNG_Table WERT |
| STAT_EKK_MOTOR_RUECKLESELEITUNG_TEXT | string | tbd table EKK_MOTOR_RUECKLESELEITUNG_Table TEXT |
| STAT_EKK_UNTERTEMPERATUR_SCHUTZ | int | 0=kein Untertemperaturschutz, 1=Untertemperaturschutz - INV Temperatur unter -10°C |
| STAT_EKK_ANFORDERUNG_VENTIL_OEFFNEN_WERT | int | tbd table EKK_ANFORDERUNG_VENTIL_OEFFNEN_Table WERT |
| STAT_EKK_ANFORDERUNG_VENTIL_OEFFNEN_TEXT | string | tbd table EKK_ANFORDERUNG_VENTIL_OEFFNEN_Table TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-drehzahl"></a>
### STEUERN_DREHZAHL

Ansteuern Drehzahl EKK KWP2000: $30 InputOutputControlByLocalIdentifier $01 Drehzahl $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_EKK_DREHZAHL_PROZENT | int | gewuenschte Drehzahl Bereich: 0 bis 100 % default = 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stat-ekk-gw-sw"></a>
### _STAT_EKK_GW_SW

Liest alle Status für EKK Entwicklerjob mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REVOLUTION_WERT | real | tbd Bereich von 0 [1/min] bis 8600 [1/min] |
| STAT_REVOLUTION_EINH | string | tbd Einheit: 1/min |
| STAT_STATUS1_MAINPOWERSUPPLY_WERT | int | tbd table Status_Diag1_MainpowerSupply WERT |
| STAT_STATUS1_MAINPOWERSUPPLY_TEXT | string | tbd table Status_Diag1_MainpowerSupply TEXT |
| STAT_STATUS1_OUTPUT_WERT | int | tbd table Status_Diag1_Output WERT |
| STAT_STATUS1_OUTPUT_TEXT | string | tbd table Status_Diag1_Output TEXT |
| STAT_STATUS1_LOAD_WERT | int | tbd table Status_Diag1_Load WERT |
| STAT_STATUS1_LOAD_TEXT | string | tbd table Status_Diag1_Load TEXT |
| STAT_STATUS1_COMMUNICATION_WERT | int | tbd table Status_Diag1_Communication WERT |
| STAT_STATUS1_COMMUNICATION_TEXT | string | tbd table Status_Diag1_Communication TEXT |
| STAT_STATUS2_STARTABILITY_WERT | int | tbd table Status_Diag2_Startability WERT |
| STAT_STATUS2_STARTABILITY_TEXT | string | tbd table Status_Diag2_Startability TEXT |
| STAT_STATUS2_INTERNAL_SUPPLY_WERT | int | tbd table Status_Diag2_Internal_Supply WERT |
| STAT_STATUS2_INTERNAL_SUPPLY_TEXT | string | tbd table Status_Diag2_Internal_Supply TEXT |
| STAT_STATUS2_STB_JAMMING | int | tbd |
| STAT_SRATUS2_STB_STATUS | int | tbd |
| STAT_STATUS2_INVERTER_OVERHEAT_WERT | int | tbd table Status_Diag2_Overheat WERT |
| STAT_STATUS2_INVERTER_OVERHEAT_TEXT | string | tbd table Status_Diag2_Overheat TEXT |
| STAT_INPUT_POWER_WERT | real | tbd Bereich von 0 [Watt] bis 12750 [Watt] |
| STAT_INPUT_POWER_EINH | string | tbd Einheit: Watt |
| STAT_MOTOR_CURRENT_WERT | real | tbd Bereich von 0 [Ampere] bis 25.4 [Ampere] |
| STAT_MOTOR_CURRENT_EINH | string | tbd Einheit: Ampere |
| STAT_TEMPERATUR_WERT | real | tbd Bereich von 0 [Grad] bis 127 [Grad] |
| STAT_TEMPERATUR_EINH | string | tbd Einheit: Grad |
| STAT_HIGH_VOLTAGE_WERT | real | tbd Bereich von 100 [Volt] bis 608 [Volt] |
| STAT_HIGH_VOLTAGE_EINH | string | tbd Einheit: Volt |
| STAT_LOW_VOLTAGE_WERT | real | tbd Bereich von 0 [Volt] bis 25.4 [Volt] |
| STAT_LOW_VOLTAGE_EINH | string | tbd Einheit: Volt |
| STAT_PRESSURE_ERROR_WERT | int | tbd table High_pressusre_control WERT |
| STAT_PRESSURE_ERROR_TEXT | string | tbd table High_pressusre_control TEXT |
| STAT_PWLI_OVER_CURRENT | int | tbd |
| STAT_PWLI_LOW_VOLTAGE | int | tbd |
| STAT_PWLI_HIGH_TEMPERATURE | int | tbd |
| STAT_PWLI_LIMIT_OF_PEB | int | tbd |
| STAT_PWLI_HIGH_PRESSURE | int | tbd |
| STAT_PWLI_LOW_TEMPERATURE | int | tbd |
| STAT_PWLI_LOW_PRESSURE | int | tbd |
| STAT_PWLI_IGBT_SHORT | int | tbd |
| STAT_PWLI_SCI_ERROR_GW_TO_INV | int | tbd |
| STAT_PWLI_SCI_ERROR_INV_TO_GW | int | tbd |
| STAT_SWO_LOW_VOLTAGE | int | tbd |
| STAT_SWO_OVER_VOLTAGE | int | tbd |
| STAT_SWO_OVER_TEMPERATURE | int | tbd |
| STAT_SWO_SHORT_CIRCUIT | int | tbd |
| STAT_SWO_OPEN_LINE | int | tbd |
| STAT_SWO_OVER_CURRENT_ON_ACTIVE | int | tbd |
| STAT_SWO_OVER_CURRENT_AT_START | int | tbd |
| STAT_SWO_CAN_COMMUNICATION_ERROR | int | tbd |
| STAT_SWO_PRESSURE_SIGNAL_ERROR | int | tbd |
| STAT_RPM_EKK_AVL_WERT | real | Bereich von 0 [%] bis 100 [%] |
| STAT_RPM_EKK_AVL_EINH | string | Einheit: % |
| STAT_PWR_ACCM_EL_AVL_WERT | real | Bereich von 0 [Kilowatt] bis 10.16 [Kilowatt] |
| STAT_PWR_ACCM_EL_AVL_EINH | string | Einheit: Kilowatt |
| STAT_ST_ACCM_EL_WERT | int | table CompStatus WERT |
| STAT_ST_ACCM_EL_TEXT | string | table CompStatus TEXT |
| STAT_ST_URA_ACCM_EL_WERT | int | table HighVoltageStatus WERT |
| STAT_ST_URA_ACCM_EL_TEXT | string | table HighVoltageStatus TEXT |
| STAT_TARGET_REVOLUTION_WERT | real | Bereich von 0 [1/min] bis 8600 [1/min] |
| STAT_TARGET_REVOLUTION_EINH | string | Einheit: 1/min |
| STAT_TARGET_STB_WERT | int | table CompEnable WERT |
| STAT_TARGET_STB_TEXT | string | table CompEnable TEXT |
| STAT_PWLI_STAT_WERT | int | tbd table PowerLimit WERT |
| STAT_PWLI_STAT_TEXT | string | tbd table PowerLimit TEXT |
| STAT_SWO_AUTOMATIC_RECOVERY | int | tbd |
| STAT_SWO_RESET_COMMAND | int | tbd |
| STAT_SWO_STAT_WERT | int | tbd table CompStop WERT |
| STAT_SWO_STAT_TEXT | string | tbd table CompStop TEXT |
| STAT_VALVE_OPEN_WERT | int | table EKK_ANFORDERUNG_VENTIL_OEFFNEN_Table WERT |
| STAT_VALVE_OPEN_TEXT | string | table EKK_ANFORDERUNG_VENTIL_OEFFNEN_Table TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kurzschluss-uvw-ekk"></a>
### STEUERN_KURZSCHLUSS_UVW_EKK

Ausfuehren IGBT_SHORT EKK KWP2000: $30 InputOutputControlByLocalIdentifier $02 IGBT_Short $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KURZSCHLUSS_UVW_EKK | int | Durchfuerung IGBT_Short Starten: 1 oder Stoppen: 0 default = 0 |

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
- [LIEFERANTEN](#table-lieferanten) (114 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (30 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (12 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [COMPSTATUS](#table-compstatus) (5 × 2)
- [SPECIAL](#table-special) (1 × 15)
- [COMPENABLE](#table-compenable) (3 × 2)
- [HIGHVOLTAGEREADY](#table-highvoltageready) (6 × 2)
- [EKK_HOCHVOLT_TABLE](#table-ekk-hochvolt-table) (5 × 2)
- [EKK_UEBERLAST_TABLE](#table-ekk-ueberlast-table) (9 × 2)
- [EKK_KOMMUNIKATION_INTERN_TABLE](#table-ekk-kommunikation-intern-table) (3 × 2)
- [EKK_STARTBEDINGUNG_TABLE](#table-ekk-startbedingung-table) (5 × 2)
- [EKK_WECHSELRICHTER_UEBERHITZUNG_TABLE](#table-ekk-wechselrichter-ueberhitzung-table) (5 × 2)
- [EKK_MOTOR_RUECKLESELEITUNG_TABLE](#table-ekk-motor-rueckleseleitung-table) (5 × 2)
- [EKK_ANFORDERUNG_VENTIL_OEFFNEN_TABLE](#table-ekk-anforderung-ventil-oeffnen-table) (5 × 2)

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

Dimensions: 114 rows × 2 columns

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
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 30 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA9C8 | Hochspannung Unterspannung |
| 0xA9C9 | Hochspannung Überspannung |
| 0xA9CA | Hochspannung ausserhalb Toleranz |
| 0xA9CB | Inverter Temperatur unzulässig |
| 0xA9CC | Fehler Temperatursensor |
| 0xA9CD | Leistungsausgang Kurzschluss |
| 0xA9CE | Leistungsausgang Unterbrechung |
| 0xA9CF | Fehler Sensor Ausgangsstrom |
| 0xA9D1 | Überlast |
| 0xA9D2 | Interner Kommunikationsfehler CRC |
| 0xA9D3 | Interner Kommunikationsfehler |
| 0xA9D4 | Hochlauf gestört |
| 0xA9D5 | Überdruck Kühlmittel |
| 0xA9D6 | Überspannung 12 Volt Versorgung |
| 0xA9D7 | Unterspannung 12 Volt Versorgung |
| 0xA9D8 | ECU Selbsttest |
| 0xA9D9 | Unterdruck Kühlmittel |
| 0xA9DA | Funktionseinschränkung wegen Begrenzung Motorstrom - temporäre Situation - Kompressor Tausch nicht erforderlich! |
| 0xA9DB | Funktionseinschränkung wegen Spannungsbegrenzung - temporäre Situation - Kompressor Tausch nicht erforderlich! |
| 0xA9DC | Funktionseinschränkung wegen Übertemperatur Inverter - temporäre Situation - Kompressor Tausch nicht erforderlich! |
| 0xA9DD | Funktionseinschränkung wegen Leistungsbegrenzung - temporäre Situation - Kompressor Tausch nicht erforderlich! |
| 0xDCC4 | PT-CAN Bus: Kommunikationsfehler |
| 0xDCC6 | Botschaft (ID 310h, Aussentemperatur/Referenzzeit): Zeitüberwachung |
| 0xDCC7 | Botschaft (ID 29Ch, Freigabe Klimakompressor Elektrisch): Zeitüberwachung |
| 0xDCC8 | Botschaft (ID 330h, Kilometerstand): Zeitüberwachung |
| 0xDCC9 | Botschaft (ID 130h, Klemmenstatus): Zeitüberwachung |
| 0xDCCA | Botschaft (ID 2D2h, Status Druck Kältekreislauf): Zeitüberwachung |
| 0xDCCC | Botschaft (ID 29Dh, Steuerung Klimakompressor Elektrisch): Zeitüberwachung |
| 0xDCCD | Botschaft (ID 2B7h, Status Hochvoltbatterie): Zeitüberwachung |
| 0xFFFF | Unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | ja |
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
| default | SPECIAL | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Datum | Tag | high | unsigned int | - | 1 | 1 | 0 |
| 0x02 | Spannung Klemme 15 | Volt | - | unsigned char | - | 0.1 | 1 | 0 |
| 0x03 | Kompressor Drehzahl | 1/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x04 | Kompressor Strom | Ampere | - | unsigned char | - | 0.1 | 1 | 0 |
| 0x05 | Kompressor Photo-Temperatur | Grad | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Kompressor Status generell | 0-n | - | 0x03 | CompStatus | 1 | 1 | 0 |
| 0x07 | Kompressor Anforderung | 0-n | - | 0x01 | CompEnable | 1 | 1 | 0 |
| 0x08 | Drehzahlanforderung Kompressor | 1/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x09 | Hochspannung bereit | 0-n | - | 0x07 | HighVoltageReady | 1 | 1 | 0 |
| 0x0A | Hochspannung Wert | Volt | - | unsigned char | - | 2 | 1 | 0 |
| 0x0B | Motor Strom | Ampere | - | unsigned char | - | 0.1 | 1 | 0 |
| 0xFF | ohne Bedeutung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | Unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | Unbekannter Fehlerort |

<a id="table-compstatus"></a>
### COMPSTATUS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kompressor AUS |
| 0x01 | Kompressor START |
| 0x02 | Kompressor EIN |
| 0x03 | unerwarteter Wert |
| 0xFF | Unbekannter Fehlerort |

<a id="table-special"></a>
### SPECIAL

Dimensions: 1 rows × 15 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 14 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0xFF | 0x07 | 0xFF | 0x08 | 0x09 | 0xFF | 0x0A | 0x0B |

<a id="table-compenable"></a>
### COMPENABLE

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kompressor sperren |
| 0x01 | Kompressor freigeben |
| 0xFF | Unbekannter Fehlerort |

<a id="table-highvoltageready"></a>
### HIGHVOLTAGEREADY

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Hochspannung AUS |
| 0x01 | Hochspannung Start Anforderung |
| 0x02 | Hochspannung EIN |
| 0x03 | Hochspannung EIN Fehler |
| 0x04 | Hochspannung EIN Fehler |
| 0xFF | Unbekannter Fehlerort |

<a id="table-ekk-hochvolt-table"></a>
### EKK_HOCHVOLT_TABLE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x40 | Hochspannung Unterspannung |
| 0x80 | Hochspannung Überspannung |
| 0xC0 | Hochspannung ausserhalb Toleranz |
| 0xFF | Unbekannter Fehlerort |

<a id="table-ekk-ueberlast-table"></a>
### EKK_UEBERLAST_TABLE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x02 | Drehzahlbegrenzung durch Spannungsversorgung |
| 0x04 | Drehzahlbegrenzung durch Motorstrom |
| 0x06 | Software Überstrom |
| 0x08 | Überlast |
| 0x0A | unerwarteter Wert |
| 0x0C | unerwarteter Wert |
| 0x0E | unerwarteter Wert |
| 0xFF | Unbekannter Fehlerort |

<a id="table-ekk-kommunikation-intern-table"></a>
### EKK_KOMMUNIKATION_INTERN_TABLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Interner Kommunikationsfehler CRC |
| 0xFF | Unbekannter Fehlerort |

<a id="table-ekk-startbedingung-table"></a>
### EKK_STARTBEDINGUNG_TABLE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x40 | Fehler einschaltverhindernd |
| 0x80 | unerwarteter Wert |
| 0xC0 | Hochlauf gestört |
| 0xFF | Unbekannter Fehlerort |

<a id="table-ekk-wechselrichter-ueberhitzung-table"></a>
### EKK_WECHSELRICHTER_UEBERHITZUNG_TABLE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | unerwarteter Wert |
| 0x02 | Inverter Temperatur unzulässig |
| 0x03 | Fehler Temperatursensor |
| 0xFF | Unbekannter Fehlerort |

<a id="table-ekk-motor-rueckleseleitung-table"></a>
### EKK_MOTOR_RUECKLESELEITUNG_TABLE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x10 | Leistungsausgang Kurzschluss |
| 0x20 | Leistungsausgang Unterbrechung |
| 0x30 | Leistungsausgang ausser Toleranz |
| 0xFF | Unbekannter Fehlerort |

<a id="table-ekk-anforderung-ventil-oeffnen-table"></a>
### EKK_ANFORDERUNG_VENTIL_OEFFNEN_TABLE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Anforderung zum Öffnen des Ventils |
| 0x01 | Anforderung zum Öffnen des Ventils |
| 0x02 | unerwarteter Wert |
| 0x03 | ungültig |
| 0xFF | Unbekannter Fehlerort |
