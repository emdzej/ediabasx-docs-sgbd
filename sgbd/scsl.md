# scsl.prg

- Jobs: [64](#jobs)
- Tables: [19](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Satellit C-Saeule links |
| ORIGIN | BMW EE-211 Robert Schmidt |
| REVISION | 0.51 |
| AUTHOR | BMW EE-211 Robert Schmidt |
| COMMENT | N/A |
| PACKAGE | 0.14 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_AEI_LESEN](#job-c-aei-lesen) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_SCHREIBEN](#job-c-aei-schreiben) - Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_AUFTRAG](#job-c-aei-auftrag) - Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PROGRAMM_REFERENZ_BACKUP_LESEN](#job-programm-referenz-backup-lesen) - Auslesen des Backups der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2500 ProgrammReferenzBackup Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HardwareReferenz Modus  : Default
- [PROGRAMM_REFERENZ_LESEN](#job-programm-referenz-lesen) - Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DatenReferenz Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [AUTHENTISIERUNG_ZUFALLSZAHL_LESEN](#job-authentisierung-zufallszahl-lesen) - Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default
- [AUTHENTISIERUNG_START](#job-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [FLASH_SIGNATUR_PRUEFEN](#job-flash-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Seuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory oder alternativ KWP2000: $18 ReadDiagnosticTroubleCodesByStatus $04 requestetIdentifiedShadowMemoryDTCAndStatus
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [AUSGABE_HISTOGRAMM_LI_ODER_X](#job-ausgabe-histogramm-li-oder-x) - Ausgabe des Histogramms fuer x oder delta-V links KWP2000: $31 Steuergeraetespezifische Routine starten $A0 Ausgabe des Histogramms fuer x oder delta-V links Modus  : Default
- [AUSGABE_HISTOGRAMM_RE_ODER_Y](#job-ausgabe-histogramm-re-oder-y) - Ausgabe des Histogramms fuer y oder delta-V rechts KWP2000: $31 Steuergeraetespezifische Routine starten $A1 Ausgabe des Histogramms fuer y oder delta-V rechts Modus  : Default
- [LOESCHEN_HISTOGRAMM_LI_ODER_X](#job-loeschen-histogramm-li-oder-x) - Loeschen des Histogramms fuer x oder delta-V links KWP2000: $31 Steuergeraetespezifische Routine starten $A2 Loeschen des Histogramms fuer x oder delta-V links Modus  : Default
- [LOESCHEN_HISTOGRAMM_RE_ODER_Y](#job-loeschen-histogramm-re-oder-y) - Loeschen des Histogramms fuer y oder delta-V rechts KWP2000: $31 Steuergeraetespezifische Routine starten $A3 Ausgabe des Histogramms fuer y oder delta-V rechts Modus  : Default
- [STATUS_ZUENDKREISMODUS_SETZEN](#job-status-zuendkreismodus-setzen) - Statusvorgabe Zuendkreismodus setzen KWP2000: $31 Steuergeraetespezifische Routine starten $2B Statusvorgabe Zuendkreismodus setzen Modus  : Default
- [STATUS_ZUENDKREISTESTABLAUF_STARTEN](#job-status-zuendkreistestablauf-starten) - Statusvorgabe Zuendkreis-Testablauf starten KWP2000: $31 Steuergeraetespezifische Routine starten $2C Statusvorgabe Zuendkreis-Testsequenzen starten Modus  : Default
- [RECYCLING_ZUEPI](#job-recycling-zuepi) - Der Job RECYCLING_ZUEPI veranlasst nach erfolgreichem setzen des ALARM-Pulses ueber Einspeisung an den dV- Sensoren am SIM und dem Uebertragen eines Fzg.individuellen Codes ein Zuenden noch vorhandener Zuendpillen durch das Steuergeraet. KWP2000: $31 Steuergeraetespezifische Routine starten $2D Recycling der Zuendpillen Modus  : Default
- [STATUS_ZURUECKNEHMEN_STEUERGERAETESTATUS](#job-status-zuruecknehmen-steuergeraetestatus) - Statusvorgaben zuruecknehmen KWP2000: $31 Steuergeraetespezifische Routine starten $20 Statusvorgaben zuruecknehmen $yz Status $yz zuruecknehmen Modus  : Default
- [STATUS_KOMMUNIKATIONSTEST_SENDE_EMPFANG_ANSTOSSEN](#job-status-kommunikationstest-sende-empfang-anstossen) - Statusvorgabe: Kommunikationstest Sende Empfang anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $27 Kommunikationstest Sende Empfang anstossen Modus  : Default
- [STATUS_SI_BUS_STATUS_LESEN_ANSTOSSEN](#job-status-si-bus-status-lesen-anstossen) - Statusvorgabe: SI-Bus-Status lesen anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $29 SI-Bus-Status lesen anstossen Modus  : Default
- [LAUFENDE_SG_NUMMER_SCHREIBEN](#job-laufende-sg-nummer-schreiben) - Laufende Steuergeraetenummer schreiben KWP2000: $2E SG spezifische Daten schreiben $00 Laufende Steuergeraetenummer schreiben $05 0x FF FF FF ist keine gueltige SG Nummer Modus  : Default
- [LAUFENDE_SG_NUMMER_LESEN](#job-laufende-sg-nummer-lesen) - Laufende Steuergeraetenummer lesen KWP2000: $22 SG spezifische Daten lesen $00 Laufende Steuergeraetenummer lesen $05 0x FF FF FF ist keine gueltige SG Nummer Modus  : Default
- [SYSTEMZEIT_SCHREIBEN](#job-systemzeit-schreiben) - Systemzeit schreiben KWP2000: $2E SG spezifische Daten schreiben $00 Systemzeit schreiben $02 0x FF FF FF FF FF ist keine gueltige Systemzeit Modus  : Default
- [SYSTEMZEIT_LESEN](#job-systemzeit-lesen) - Systemzeit lesen KWP2000: $22 SG spezifische Daten lesen $00 Systemzeit lesen $02 0x FF FF FF FF FF ist keine gueltige Systemzeit Modus  : Default
- [HERSTELLERDATEN_SCHREIBEN](#job-herstellerdaten-schreiben) - Herstellerdaten schreiben KWP2000: $2E SG spezifische Daten schreiben $00 Herstellerdaten schreiben $04 Modus  : Default
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Herstellerdaten lesen KWP2000: $22 SG spezifische Daten lesen $00 Herstellerdaten lesen $04 Modus  : Default
- [STATUS_SELBSTTEST_BESCHLEUNIGUNGSSENSOR_X_RICHTUNG](#job-status-selbsttest-beschleunigungssensor-x-richtung) - Selbsttest Beschleunigungssensor x-Richtung anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $21 Selbsttest Beschleunigungssensor x-Richtung anstossen Modus  : Default
- [STEUERGERAETE_STATUS_LESEN](#job-steuergeraete-status-lesen) - Steuergeraete Status lesen KWP2000: $22 SG spezifische Daten lesen $98 Steuergeraete Status lesen $00 Modus  : Default

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
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
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
| F_ORT_NR | int | Index fuer Fehlerort |
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
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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

<a id="job-programm-referenz-backup-lesen"></a>
### PROGRAMM_REFERENZ_BACKUP_LESEN

Auslesen des Backups der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2500 ProgrammReferenzBackup Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PROGRAMM_REFERENZ_BACKUP | string | letzter lauffaehiger Programmstand |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-zeiten-lesen"></a>
### FLASH_ZEITEN_LESEN

Auslesen der Flash Loeschzeit, Signaturtestzeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_LOESCHZEIT | int | Flash Loeschzeit in Sekunden |
| FLASH_SIGNATURTESTZEIT | int | Flash Signaturtestzeit in Sekunden |
| FLASH_RESETZEIT | int | Flash Resetzeit in Sekunden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hardware-referenz-lesen"></a>
### HARDWARE_REFERENZ_LESEN

Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HardwareReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HARDWARE_REFERENZ | string | Hardware Referenz |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-programm-referenz-lesen"></a>
### PROGRAMM_REFERENZ_LESEN

Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PROGRAMM_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-daten-referenz-lesen"></a>
### DATEN_REFERENZ_LESEN

Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DatenReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN_REFERENZ | string | Daten Referenz |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-zufallszahl-lesen"></a>
### AUTHENTISIERUNG_ZUFALLSZAHL_LESEN

Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEVEL | int |  |
| USER_ID | long | optional |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ZUFALLSZAHL | binary | Zufallszahl |
| AUTHENTISIERUNG | string | Authentisierungsart 'Keine'        Keine Authentisierung 'Simple'       Einfache Authentisierung 'Symetrisch'   Symetrische Authentisierung 'Asymetrisch'  Asymetrische Authentisierung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-start"></a>
### AUTHENTISIERUNG_START

Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL | binary | Schluessel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-programmier-status-lesen"></a>
### FLASH_PROGRAMMIER_STATUS_LESEN

Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS_TEXT | string | table ProgrammierStatus STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS | int | ProgrammierStatus 0 - 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-signatur-pruefen"></a>
### FLASH_SIGNATUR_PRUEFEN

Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BEREICH | string | 'Programm' 'Daten' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Seuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 4 = Speicher loeschen nicht moeglich |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge ohne Telegramm-Overhead |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ANZAHL | int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
| FLASH_SCHREIBEN_STATUS | int | Programmierstatus 1 = Programmierung in Ordnung 2 = Programmierung nicht in Ordnung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge ohne Telegramm-Overhead |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NR | int | ==0 : aktuelles AIF &gt; 0 : Nummer des zu lesenden AIF default = 0 : aktuelles AIF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ADRESSE | long | AIF Adresse |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_PROGRAMMIER_DATUM | string | Datum der SG-Programmierung in der Form JJJJ.MM.TT |
| AIF_ZUSAMMENBAU_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_DATENSATZ_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_TESTER_NR | string | Tester Seriennummer |
| AIF_KM_STAND | long | km-Stand bei der Programmierung |
| AIF_PROGRAMM_STAND | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_PROGRAMMIER_DATUM | string | Datum der SG-Programmierung in der Form JJJJ.MM.TT |
| AIF_ZUSAMMENBAU_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_DATENSATZ_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_TESTER_NR | string | Tester Seriennummer |
| AIF_KM_STAND | long | km-Stand bei der Programmierung |
| AIF_PROGRAMM_STAND | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AIF_NR | int | Nummer des geschreibenen AIF |
| AIF_DATEN | binary | AIF Hex-Daten |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG AIF lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG AIF lesen |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory oder alternativ KWP2000: $18 ReadDiagnosticTroubleCodesByStatus $04 requestetIdentifiedShadowMemoryDTCAndStatus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

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
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ausgabe-histogramm-li-oder-x"></a>
### AUSGABE_HISTOGRAMM_LI_ODER_X

Ausgabe des Histogramms fuer x oder delta-V links KWP2000: $31 Steuergeraetespezifische Routine starten $A0 Ausgabe des Histogramms fuer x oder delta-V links Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ausgabe-histogramm-re-oder-y"></a>
### AUSGABE_HISTOGRAMM_RE_ODER_Y

Ausgabe des Histogramms fuer y oder delta-V rechts KWP2000: $31 Steuergeraetespezifische Routine starten $A1 Ausgabe des Histogramms fuer y oder delta-V rechts Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-loeschen-histogramm-li-oder-x"></a>
### LOESCHEN_HISTOGRAMM_LI_ODER_X

Loeschen des Histogramms fuer x oder delta-V links KWP2000: $31 Steuergeraetespezifische Routine starten $A2 Loeschen des Histogramms fuer x oder delta-V links Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-loeschen-histogramm-re-oder-y"></a>
### LOESCHEN_HISTOGRAMM_RE_ODER_Y

Loeschen des Histogramms fuer y oder delta-V rechts KWP2000: $31 Steuergeraetespezifische Routine starten $A3 Ausgabe des Histogramms fuer y oder delta-V rechts Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zuendkreismodus-setzen"></a>
### STATUS_ZUENDKREISMODUS_SETZEN

Statusvorgabe Zuendkreismodus setzen KWP2000: $31 Steuergeraetespezifische Routine starten $2B Statusvorgabe Zuendkreismodus setzen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODUS_NR | int | Modus-Nummer $00-$0F |
| ZUENDKREIS_NR | int | Zuendkreis-Nummer Statusvorgabe fuer Zuendkreis-Nummer x wenn Bit x=1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MESSWERT_ZK0_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 0 |
| MESSWERT_ZK1_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 1 |
| MESSWERT_ZK2_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 2 |
| MESSWERT_ZK3_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 3 |
| MESSWERT_ZK4_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 4 |
| MESSWERT_ZK5_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 5 |
| MESSWERT_ZK6_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 6 |
| MESSWERT_ZK7_DIAG_PIN | int | Messwert am Pin Diag des E100.37 fuer Zuendkreis 7 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zuendkreistestablauf-starten"></a>
### STATUS_ZUENDKREISTESTABLAUF_STARTEN

Statusvorgabe Zuendkreis-Testablauf starten KWP2000: $31 Steuergeraetespezifische Routine starten $2C Statusvorgabe Zuendkreis-Testsequenzen starten Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_NR | int | TEST-Nummer ??? tbd |
| ZUENDKREIS_NR | int | Zuendkreis-Nummer Statusvorgabe fuer Zuendkreis-Nummer x wenn Bit x=1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-recycling-zuepi"></a>
### RECYCLING_ZUEPI

Der Job RECYCLING_ZUEPI veranlasst nach erfolgreichem setzen des ALARM-Pulses ueber Einspeisung an den dV- Sensoren am SIM und dem Uebertragen eines Fzg.individuellen Codes ein Zuenden noch vorhandener Zuendpillen durch das Steuergeraet. KWP2000: $31 Steuergeraetespezifische Routine starten $2D Recycling der Zuendpillen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HI_FZG_INDIVID_CODIERUNG | int | Fahrzeugindividuelle Codierung High Byte |
| LO_FZG_INDIVID_CODIERUNG | int | Fahrzeugindividuelle Codierung Low Byte |
| ZUENDKREISNUMMER | int | Nummer des auszuloesenden Zuendkreises 1 bis 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zuruecknehmen-steuergeraetestatus"></a>
### STATUS_ZURUECKNEHMEN_STEUERGERAETESTATUS

Statusvorgaben zuruecknehmen KWP2000: $31 Steuergeraetespezifische Routine starten $20 Statusvorgaben zuruecknehmen $yz Status $yz zuruecknehmen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_ID | int | ID des zurueck zu nehmenden Status $00 = alle Stati zuruecknehmen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kommunikationstest-sende-empfang-anstossen"></a>
### STATUS_KOMMUNIKATIONSTEST_SENDE_EMPFANG_ANSTOSSEN

Statusvorgabe: Kommunikationstest Sende Empfang anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $27 Kommunikationstest Sende Empfang anstossen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATENBYTE_1 | int | Frei waehlbares Datenbyte 1 |
| DATENBYTE_2 | int | Frei waehlbares Datenbyte 2 |
| DATENBYTE_3 | int | Frei waehlbares Datenbyte 3 |
| DATENBYTE_4 | int | Frei waehlbares Datenbyte 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DATENBYTE_1 | int | Rueckantwort des Datenbyte 1 |
| STAT_DATENBYTE_2 | int | Rueckantwort des Datenbyte 2 |
| STAT_DATENBYTE_3 | int | Rueckantwort des Datenbyte 3 |
| STAT_DATENBYTE_4 | int | Rueckantwort des Datenbyte 4 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-si-bus-status-lesen-anstossen"></a>
### STATUS_SI_BUS_STATUS_LESEN_ANSTOSSEN

Statusvorgabe: SI-Bus-Status lesen anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $29 SI-Bus-Status lesen anstossen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SI_BUS_ID | int | Zu lesende SI-Bus-ID |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAENGE | int | Anzahl der Datenbytes in der Rueckantwort |
| STAT_DATENBYTES | binary | Rueckantwort Datenbytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-laufende-sg-nummer-schreiben"></a>
### LAUFENDE_SG_NUMMER_SCHREIBEN

Laufende Steuergeraetenummer schreiben KWP2000: $2E SG spezifische Daten schreiben $00 Laufende Steuergeraetenummer schreiben $05 0x FF FF FF ist keine gueltige SG Nummer Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| L_SG_NR_BYTE_1 | int | Laufende Steuergeraetenummer Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| L_SG_NR_BYTE_2 | int | Laufende Steuergeraetenummer Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| L_SG_NR_BYTE_3 | int | Laufende Steuergeraetenummer Byte 3 0x0 - 0xFF bzw. 0 - 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-laufende-sg-nummer-lesen"></a>
### LAUFENDE_SG_NUMMER_LESEN

Laufende Steuergeraetenummer lesen KWP2000: $22 SG spezifische Daten lesen $00 Laufende Steuergeraetenummer lesen $05 0x FF FF FF ist keine gueltige SG Nummer Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| L_SG_NR_BYTE_1 | int | Laufende Steuergeraetenummer Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| L_SG_NR_BYTE_2 | int | Laufende Steuergeraetenummer Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| L_SG_NR_BYTE_3 | int | Laufende Steuergeraetenummer Byte 3 0x0 - 0xFF bzw. 0 - 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemzeit-schreiben"></a>
### SYSTEMZEIT_SCHREIBEN

Systemzeit schreiben KWP2000: $2E SG spezifische Daten schreiben $00 Systemzeit schreiben $02 0x FF FF FF FF FF ist keine gueltige Systemzeit Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SZ_BYTE_1 | int | Systemzeit Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_2 | int | Systemzeit Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_3 | int | Systemzeit Byte 3 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_4 | int | Systemzeit Byte 4 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_5 | int | Systemzeit Byte 5 0x0 - 0xFF bzw. 0 - 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemzeit-lesen"></a>
### SYSTEMZEIT_LESEN

Systemzeit lesen KWP2000: $22 SG spezifische Daten lesen $00 Systemzeit lesen $02 0x FF FF FF FF FF ist keine gueltige Systemzeit Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SZ_BYTE_1 | int | Systemzeit Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_2 | int | Systemzeit Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_3 | int | Systemzeit Byte 3 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_4 | int | Systemzeit Byte 4 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_5 | int | Systemzeit Byte 5 0x0 - 0xFF bzw. 0 - 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-schreiben"></a>
### HERSTELLERDATEN_SCHREIBEN

Herstellerdaten schreiben KWP2000: $2E SG spezifische Daten schreiben $00 Herstellerdaten schreiben $04 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HD_BYTE_1 | int | Herstellerdaten Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_2 | int | Herstellerdaten Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_3 | int | Herstellerdaten Byte 3 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_4 | int | Herstellerdaten Byte 4 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_5 | int | Herstellerdaten Byte 5 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_6 | int | Herstellerdaten Byte 6 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_7 | int | Herstellerdaten Byte 7 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_8 | int | Herstellerdaten Byte 8 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_9 | int | Herstellerdaten Byte 9 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_10 | int | Herstellerdaten Byte 10 0x0 - 0xFF bzw. 0 - 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Herstellerdaten lesen KWP2000: $22 SG spezifische Daten lesen $00 Herstellerdaten lesen $04 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HD_BYTE_1 | int | Herstellerdaten Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_2 | int | Herstellerdaten Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_3 | int | Herstellerdaten Byte 3 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_4 | int | Herstellerdaten Byte 4 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_5 | int | Herstellerdaten Byte 5 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_6 | int | Herstellerdaten Byte 6 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_7 | int | Herstellerdaten Byte 7 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_8 | int | Herstellerdaten Byte 8 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_9 | int | Herstellerdaten Byte 9 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_10 | int | Herstellerdaten Byte 10 0x0 - 0xFF bzw. 0 - 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-selbsttest-beschleunigungssensor-x-richtung"></a>
### STATUS_SELBSTTEST_BESCHLEUNIGUNGSSENSOR_X_RICHTUNG

Selbsttest Beschleunigungssensor x-Richtung anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $21 Selbsttest Beschleunigungssensor x-Richtung anstossen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-status-lesen"></a>
### STEUERGERAETE_STATUS_LESEN

Steuergeraete Status lesen KWP2000: $22 SG spezifische Daten lesen $98 Steuergeraete Status lesen $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_READINESS_FLAG | int | Bit 0: Bus aktiv (&gt;16sek. seit letztem Loeschen) Bit 1: Pre-Drive-Check vollstaendig durchgefuehrt Bit 2: System betriebsfaehig, d. h. Klemme R ein und Pre-Drive-Check erfolgt Bit 3: System wurde abgeschaltet Bit 4: Klemme 15 ein Bit 5: frei Bit 6: frei Bit 7: frei |
| STAT_KLEMMENSTATUS_BUS | int | tbd ??? |
| STAT_KM_HIGH | int | aktueller Kilometerstand High-Byte |
| STAT_KM_LOW | int | aktueller Kilometerstand Low-Byte |
| STAT_WIDERSTAND_ZK_1 | int | Zuordnung Codierwert-Widerstand: CW = 50*R-40 0.84 &lt;= R/Ohm &lt;= 5.88 0x02 &lt;= R/Ohm &lt;= 0xFD 0x00 Widerstand der Zuendpille seit letztem POR noch nicht gemessen 0x01 Widerstand der Zuendpille kleiner 0.84 Ohm 0x02 - 0xFD Gueltiger Widerstandsbereich in 20 mOhm Schritten 0xFE Widerstand der Zuendpille ist groesser als 5.88 Ohm 0xFF Fehler beim Messen des Zuendpillenwiderstands |
| STAT_ZUENDKREIS_1_A | int | Bit 0: Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK1 Bit 1: Kurzschluss ZK1 nach Masse Bit 2: Kurzschluss ZK1 nach Plus Bit 3: Widerstand Zuendpille ZK1 zu klein Bit 4: Widerstand Zuendpille ZK1 zu gross Bit 5: Unterbrechung ZK1 Bit 6: Spannung ZK1 n.i.O. Bit 7: Zuendkondensator ZK1 n.i.O. |
| STAT_ZUENDKREIS_1_B | int | Bit 0: Codierung / Konfiguration ZK1 unstimmig Bit 1: sonstige Fehler ZK1 Bit 2: frei Bit 3: frei Bit 4: frei Bit 5: frei Bit 6: frei Bit 7: frei |
| STAT_WIDERSTAND_ZK_2 | int | Zuordnung Codierwert-Widerstand: CW = 50*R-40 0.84 &lt;= R/Ohm &lt;= 5.88 0x02 &lt;= R/Ohm &lt;= 0xFD 0x00 Widerstand der Zuendpille seit letztem POR noch nicht gemessen 0x01 Widerstand der Zuendpille kleiner 0.84 Ohm 0x02 - 0xFD Gueltiger Widerstandsbereich in 20 mOhm Schritten 0xFE Widerstand der Zuendpille ist groesser als 5.88 Ohm 0xFF Fehler beim Messen des Zuendpillenwiderstands |
| STAT_ZUENDKREIS_2_A | int | Bit 0: Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK2 Bit 1: Kurzschluss ZK2 nach Masse Bit 2: Kurzschluss ZK2 nach Plus Bit 3: Widerstand Zuendpille ZK2 zu klein Bit 4: Widerstand Zuendpille ZK2 zu gross Bit 5: Unterbrechung ZK2 Bit 6: Spannung ZK2 n.i.O. Bit 7: Zuendkondensator ZK2 n.i.O. |
| STAT_ZUENDKREIS_2_B | int | Bit 0: Codierung / Konfiguration ZK2 unstimmig Bit 1: sonstige Fehler ZK2 Bit 2: frei Bit 3: frei Bit 4: frei Bit 5: frei Bit 6: frei Bit 7: frei |
| STAT_OFFSET_BESCHLEUNIGUNGSSENSOR | int |  |
| STAT_MESSWERT_BESCHLEUNIGUNGSSENSOR_AKTUELL | int |  |
| STAT_WERT_INTEGRAL_1_AKTUELL | int |  |
| STAT_WERT_INTEGRAL_2_AKTUELL | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (71 × 2)
- [LIEFERANTEN](#table-lieferanten) (50 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (12 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (4 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (4 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (10 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (58 × 2)
- [IORTTEXTE](#table-iorttexte) (58 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 71 rows × 2 columns

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
| ?8A? | ERROR_LARGE_UIF_FOUND |
| ?8B? | ERROR_SMALL_UIF_FOUND |
| ?8C? | ERROR_NO_FREE_UIF |
| ?8D? | ERROR_MAX_UIF |
| ?8E? | ERROR_LEVEL |
| ?8F? | ERROR_KEY |
| ?90? | ERROR_AUTHENTICATION |
| ?91? | ERROR_FLASH_SIGNATURE_METHOD |
| ?92? | ERROR_SIZE_UIF |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 50 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
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
| 0x28 | BERU (DODUCO) |
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

Dimensions: 12 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

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

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 12300000 |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 1xxxxxxx | 11 | Fehlerklassifikation  t &gt; 1min |
| x1xxxxxx | 21 | Fehlerklassifikation 1s &lt; t &lt; 1min |
| xx1xxxxx | 31 | Fehlerklassifikation 0 &lt; t &lt; 1s |
| xxxxxxxx | 0 | -- |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 12300000 |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 1xxxxxxx | 11 | Fehlerklassifikation  t &gt; 1min |
| x1xxxxxx | 21 | Fehlerklassifikation 1s &lt; t &lt; 1min |
| xx1xxxxx | 31 | Fehlerklassifikation 0 &lt; t &lt; 1s |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | - | - |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Systemzeit Fehlerbeginn | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0x02 | Systemzeit Fehlerende | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0xXY | unbekannte UW | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Systemzeit Fehlerbeginn | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0x02 | Systemzeit Fehlerende | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0xXY | unbekannte UW | 1 | - | unsigned char | - | 1 | 1 | 0 |

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

<a id="table-speichersegment"></a>
### SPEICHERSEGMENT

Dimensions: 10 rows × 3 columns

| SEG_BYTE | SEG_NAME | SEG_TEXT |
| --- | --- | --- |
| 0x00 | LAR | linearAdressRange |
| 0x01 | ROMI | ROM / EPROM, internal |
| 0x02 | ROMX | ROM / EPROM, external |
| 0x03 | NVRAM | NV-RAM (characteristic zones, DTC memory |
| 0x04 | RAMIS | RAM, internal (short MOV) |
| 0x05 | RAMXX | RAM, external (x data MOV) |
| 0x06 | FLASH | Flash EPROM |
| 0x07 | UIFM | User Info Field Memory |
| 0x0B | RAMIL | RAM, internal (long MOV / Register) |
| 0xFF | ??? | unbekanntes Speichersegment |

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Anlieferzustand |
| 0x01 | Normalbetrieb |
| 0x02 | nicht benutzt |
| 0x03 | nicht benutzt |
| 0x04 | nicht benutzt |
| 0x05 | nicht benutzt |
| 0x06 | nicht benutzt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Datenreferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vollstaendig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vollstaendig |
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

Dimensions: 58 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9928 | Watchdog-Reset uP |
| 0x9929 | Clock-Monitor-Reset uP |
| 0x992A | Illegal Opcode uP |
| 0x992B | falsche Fahrgestellnummer |
| 0x992C | Systemzeitfehler |
| 0x992D | Timeout ID 01 |
| 0x992E | Timeout ID 02 |
| 0x992F | Timeout ID 03 |
| 0x9930 | Timeout ID 04 |
| 0x9931 | Timeout ID 05 |
| 0x9932 | Timeout ID 06 |
| 0x9933 | Timeout ID 07 |
| 0x9934 | Timeout ID 08 |
| 0x9935 | Timeout ID 09 |
| 0x9936 | Timeout ID 10 |
| 0x9937 | Timeout ID 32 |
| 0x9938 | Timeout ID 33 |
| 0x9939 | Timeout ID 34 |
| 0x993A | Timeout ID 35 |
| 0x993B | Timeout ID 36 |
| 0x993C | Timeout ID 96 |
| 0x993D | Timeout ID 127 |
| 0x993E | Timeout ID 172 |
| 0x993F | Timeout ID 175 |
| 0x9940 | Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK1 |
| 0x9941 | Kurzschluss ZK1 nach Masse |
| 0x9942 | Kurzschluss ZK1 nach Plus |
| 0x9943 | Widerstand Zuendpille ZK1 zu klein |
| 0x9944 | Widerstand Zuendpille ZK1 zu gross |
| 0x9945 | Unterbrechung ZK1 |
| 0x9946 | Spannung ZK1 n. i. O. |
| 0x9947 | Zuendkondensator ZK1 n. i. O. |
| 0x9948 | Codierung / Konfiguration ZK1 unstimmig |
| 0x9949 | sonstiger Fehler ZK1 |
| 0x994A | Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK2 |
| 0x994B | Kurzschluss ZK2 nach Masse |
| 0x994C | Kurzschluss ZK2 nach Plus |
| 0x994D | Widerstand Zuendpille ZK2 zu klein |
| 0x994E | Widerstand Zuendpille ZK2 zu gross |
| 0x994F | Unterbrechung ZK2 |
| 0x9950 | Spannung ZK2 n. i. O. |
| 0x9951 | Zuendkondensator ZK2 n. i. O. |
| 0x9952 | Codierung / Konfiguration ZK2 unstimmig |
| 0x9953 | sonstiger Fehler ZK2 |
| 0x9956 | Fehler im Alarm-Pfad |
| 0x9957 | Fehler Beschleunigungssensor:Offset zu gross (x-Richtung) |
| 0x9958 | Fehler Beschleunigungssensor:Selbsttestwert zu gross (x-Richtung) |
| 0x9959 | Fehler Beschleunigungssensor:Selbsttestwert zu klein (x-Richtung) |
| 0x995A | Statusfehler Beschleunigungssensor |
| 0x99E8 | Power-On-Reset uP |
| 0x99E9 | Diagnose S/E-Modul (Lichtleistung) |
| 0x99EA | SI-Bus: Uebertragungsfehler, CRC-Fehler ERRIF |
| 0x99EB | SI-Bus: Uebertragungsfehler, Formatfehler ILLPIF |
| 0x99EC | SI-Bus: Synchronisierungspuls zu frueh SYNEIF |
| 0x99ED | SI-Bus: Synchronisierung verloren SYNLIF |
| 0x99EE | SI-Bus: Slotmismatch, Timingfehler SLMMIF |
| 0x99EF | SI-Bus: FIFO-Ueberlauf OVRNIF |
| 0x???? | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 58 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9928 | Watchdog-Reset uP |
| 0x9929 | Clock-Monitor-Reset uP |
| 0x992A | Illegal Opcode uP |
| 0x992B | falsche Fahrgestellnummer |
| 0x992C | Systemzeitfehler |
| 0x992D | Timeout ID 01 |
| 0x992E | Timeout ID 02 |
| 0x992F | Timeout ID 03 |
| 0x9930 | Timeout ID 04 |
| 0x9931 | Timeout ID 05 |
| 0x9932 | Timeout ID 06 |
| 0x9933 | Timeout ID 07 |
| 0x9934 | Timeout ID 08 |
| 0x9935 | Timeout ID 09 |
| 0x9936 | Timeout ID 10 |
| 0x9937 | Timeout ID 32 |
| 0x9938 | Timeout ID 33 |
| 0x9939 | Timeout ID 34 |
| 0x993A | Timeout ID 35 |
| 0x993B | Timeout ID 36 |
| 0x993C | Timeout ID 96 |
| 0x993D | Timeout ID 127 |
| 0x993E | Timeout ID 172 |
| 0x993F | Timeout ID 175 |
| 0x9940 | Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK1 |
| 0x9941 | Kurzschluss ZK1 nach Masse |
| 0x9942 | Kurzschluss ZK1 nach Plus |
| 0x9943 | Widerstand Zuendpille ZK1 zu klein |
| 0x9944 | Widerstand Zuendpille ZK1 zu gross |
| 0x9945 | Unterbrechung ZK1 |
| 0x9946 | Spannung ZK1 n. i. O. |
| 0x9947 | Zuendkondensator ZK1 n. i. O. |
| 0x9948 | Codierung / Konfiguration ZK1 unstimmig |
| 0x9949 | sonstiger Fehler ZK1 |
| 0x994A | Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK2 |
| 0x994B | Kurzschluss ZK2 nach Masse |
| 0x994C | Kurzschluss ZK2 nach Plus |
| 0x994D | Widerstand Zuendpille ZK2 zu klein |
| 0x994E | Widerstand Zuendpille ZK2 zu gross |
| 0x994F | Unterbrechung ZK2 |
| 0x9950 | Spannung ZK2 n. i. O. |
| 0x9951 | Zuendkondensator ZK2 n. i. O. |
| 0x9952 | Codierung / Konfiguration ZK2 unstimmig |
| 0x9953 | sonstiger Fehler ZK2 |
| 0x9956 | Fehler im Alarm-Pfad |
| 0x9957 | Fehler Beschleunigungssensor:Offset zu gross (x-Richtung) |
| 0x9958 | Fehler Beschleunigungssensor:Selbsttestwert zu gross (x-Richtung) |
| 0x9959 | Fehler Beschleunigungssensor:Selbsttestwert zu klein (x-Richtung) |
| 0x995A | Statusfehler Beschleunigungssensor |
| 0x99E8 | Power-On-Reset uP |
| 0x99E9 | Diagnose S/E-Modul (Lichtleistung) |
| 0x99EA | SI-Bus: Uebertragungsfehler, CRC-Fehler ERRIF |
| 0x99EB | SI-Bus: Uebertragungsfehler, Formatfehler ILLPIF |
| 0x99EC | SI-Bus: Synchronisierungspuls zu frueh SYNEIF |
| 0x99ED | SI-Bus: Synchronisierung verloren SYNLIF |
| 0x99EE | SI-Bus: Slotmismatch, Timingfehler SLMMIF |
| 0x99EF | SI-Bus: FIFO-Ueberlauf OVRNIF |
| 0x???? | unbekannter Fehlerort |
