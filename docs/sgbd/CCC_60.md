# CCC_60.prg

- Jobs: [80](#jobs)
- Tables: [45](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CCC_60 fuer E60 |
| ORIGIN | BMW EE-40 Dieter Vollmerhaus |
| REVISION | 2.06 |
| AUTHOR | BMW EE-40 Dieter Vollmerhaus, Siemens VDO Automotive AG CC80SD-AD Joerg Keller, Siemens VDO Automotive AG CC80SD-AD Lothar Weitzel |
| COMMENT | N/A |
| PACKAGE | 1.26 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
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
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [AUTHENTISIERUNG_ZUFALLSZAHL_LESEN](#job-authentisierung-zufallszahl-lesen) - Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default
- [AUTHENTISIERUNG_START](#job-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [FLASH_SIGNATUR_PRUEFEN](#job-flash-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [SELBSTTEST_STARTEN](#job-selbsttest-starten) - Starten des Selbsttests KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest
- [SELBSTTEST_STOPPEN](#job-selbsttest-stoppen) - Abbrechen des Selbsttests KWP2000: $32 StopRoutineByLocalIdentifier $04 Selftest
- [SELBSTTEST_ABFRAGEN](#job-selbsttest-abfragen) - Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $04 Selftest
- [SYSTEMTEST_STARTEN](#job-systemtest-starten) - Starten des Systemtests KWP2000: $31 StartRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest
- [SYSTEMTEST_STOPPEN](#job-systemtest-stoppen) - Abbrechen des Systemtests KWP2000: $32 StopRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest
- [SYSTEMTEST_ABFRAGEN](#job-systemtest-abfragen) - Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $FA OEM-spezifisch: Systemtest
- [READ_LOGISTIC_NR](#job-read-logistic-nr) - Auslesen der Logistiknummer KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [READ_WA_CODE](#job-read-wa-code) - WA-Code auslesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [SET_ENDE_CODIERUNG](#job-set-ende-codierung) - Codierdaten flashen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [SET_LOGISTIC_NR](#job-set-logistic-nr) - Modify Logistic Nr KWP2000: $2E WriteDataByCommonIdentifier Dieser job schickt zusaetzlich ein set_ende_codierung Modus  : Default
- [SER_NR_DOM_LESEN](#job-ser-nr-dom-lesen) - Seriennummer 14-stellig lesen KWP2000: $21 ReadDataByLocalIdentifier $E0 Local ID SER_NR_DOM Modus  : Default
- [SCHREIBEN_BLOCKLAENGE](#job-schreiben-blocklaenge) - max. Blocklaenge zum SW-Laden KWP2000: $2e WriteDataByCommonIdentifier Modus  : Default
- [READ_CURRENT_UIF](#job-read-current-uif) - currentUIFDataTable KWP2000: $1A ReadECUIdentification Modus  : Default
- [READ_BMW_SACH_NR](#job-read-bmw-sach-nr) - SystemSupplierECUHardwareNumber KWP2000: $1A ReadECUIdentification Modus  : Default
- [READ_BMW_HW_VERSION](#job-read-bmw-hw-version) - vehicleManufactureECUHardwareVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default
- [PROGRAM_REFERENZ_LESEN](#job-program-referenz-lesen) - vehicleManufECUSoftwareLayerVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default
- [STATUS_DISPLAY](#job-status-display) - Info ueber die aktuell verwendeten Displays KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_MEMORY_USAGE](#job-status-memory-usage) - Aktueller Verbrauch der System Recourcen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_MEMORY_AVAILABLE](#job-status-memory-available) - Groesse der verfuegbaren System Recourcen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_DVD_TEMPERATURE](#job-status-dvd-temperature) - Status der Temperatur des DVD Laufwerks KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_DRIVE_DVD](#job-status-drive-dvd) - Status des DVD-Laufwerks wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_DRIVE_CD](#job-status-drive-cd) - Status des CD-Laufwerks wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_TASTER](#job-status-taster) - Status aller Taster wird ausgegeben Die Daten koennen nur dann zurueckgeben werden, wenn der CCC in Zustand 'FIB ist aktuell' ist (s. JOB status_fib_create) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_DREHKNOPF](#job-status-drehknopf) - Der aktuelle Status des Drehknopfs wird ausgegeben Die Daten können nur dann zurueckgeben werden, wenn der CCC in Zustand 'FIB ist aktuell' ist (s. JOB status_fib_create) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_CD_SWL](#job-status-cd-swl) - Der aktuelle SWL-Status bei SWL von CD wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [SET_END_SWL](#job-set-end-swl) - Schließe Most-Lade-Prozedur ab KWP2000: $31 StartFunctionByLocalId Modus  : Default
- [GENERATE_FIB](#job-generate-fib) - Erstelle neues FastBootImage KWP2000: $31 StartFunctionByLocalId Modus  : Default
- [STATUS_FIB_CREATE](#job-status-fib-create) - aktueller Zustand des FastBootImage KWP2000: $33 GetRoutineResultByLocalId Modus  : Default
- [STEUERN_EJECT_CD](#job-steuern-eject-cd) - Falls eine CD im Laufwerk ist, wird sie ausgeworfen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STEUERN_EJECT_DVD](#job-steuern-eject-dvd) - Falls ein Medium im DVD Laufwerk ist, wird es ausgeworfen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STATUS_LESEN_LAUFWERK](#job-status-lesen-laufwerk) - Auslesen des codierten Laufwerks (CD Laufwerk oder MD Laufwerk) KWP2000: $22 ReadDataByCommonIdentifier
- [STEUERN_INTERNAL_RESET](#job-steuern-internal-reset) - Seuergeraete reset ausloesen KWP2000: $11 ECUReset $FA RequestInternalReset Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig 

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

<a id="job-fs-sperren"></a>
### FS_SPERREN

Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERREN | string | "ja"   -&gt; Fehlerspeicher sperren "nein" -&gt; Fehlerspeicher freigeben table DigitalArgument TEXT |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
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

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
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

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

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

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

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
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
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

<a id="job-zif-lesen"></a>
### ZIF_LESEN

Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_PROGRAMM_REFERENZ | string | PRGREF ProgrammReferenz letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_SG_KENNUNG | string | ZZZ |
| ZIF_PROJEKT | string | PPPxV |
| ZIF_PROGRAMM_STAND | string | BBxh |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BMW_HW | string | VMECUH*N vehicleManufacturerECUHardware*Number BMW Hardware Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

<a id="job-zif-backup-lesen"></a>
### ZIF_BACKUP_LESEN

Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_PROGRAMM_REFERENZ | string | PRGREFB ProgrammReferenzBackup letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_BACKUP_SG_KENNUNG | string | ZZZ |
| ZIF_BACKUP_PROJEKT | string | PPPxV |
| ZIF_BACKUP_PROGRAMM_STAND | string | BBxh |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BACKUP_BMW_HW | string | VMECUH*NB vehicleManufECUHW*NumberBackup BMW Hardware* Nummer |
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

<a id="job-hardware-referenz-lesen"></a>
### HARDWARE_REFERENZ_LESEN

Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HARDWARE_REFERENZ | string | Hardware Referenz Format: ZZZPPPx 7 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware |
| HW_REF_SG_KENNUNG | string | ZZZ |
| HW_REF_PROJEKT | string | PPPx |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-daten-referenz-lesen"></a>
### DATEN_REFERENZ_LESEN

Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN_REFERENZ | string | Daten Referenz Format: ZZZPPPxVBBxhdxxxx 17 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller d     : Datenstandersteller xxxx  : frei aber eindeutig belegt |
| DATEN_REF_SG_KENNUNG | string | ZZZ |
| DATEN_REF_PROJEKT | string | PPPxV |
| DATEN_REF_PROGRAMM_STAND | string | BBxh |
| DATEN_REF_DATENSATZ | string | dxxxx |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-zeiten-lesen"></a>
### FLASH_ZEITEN_LESEN

Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_LOESCHZEIT | int | Flash Loeschzeit in Sekunden |
| FLASH_SIGNATURTESTZEIT | int | Flash Signaturtestzeit in Sekunden |
| FLASH_RESETZEIT | int | Flash Resetzeit in Sekunden |
| FLASH_AUTHENTISIERZEIT | int | Flash Authentisierberechnungszeit in Sekunden |
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
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Authentisierungszeit in Sekunden Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Schluesseldaten Byte 21+Anzahl Daten: ETX (0x03) |

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
| SIGNATURTESTZEIT | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

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
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden (Byteparameter 1) Byte 5,6            : Loeschzeit in Sekunden (WordParameter 1 (low/high)) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 5 = Signaturpruefung PAF nicht durchgefuehrt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NUMMER | int | ==0 : aktuelles AIF &gt; 0 : Nummer des zu lesenden AIF default = 0 : aktuelles AIF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ADRESSE_HIGH | int | AIF Adresse des AIF, High-Word |
| AIF_ADRESSE_LOW | int | AIF Adresse des AIF, Low-Word |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| AIF_GROESSE | int | Groesse des AIF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig oder 17-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ oder TTMMJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AIF_NUMMER | int | Nummer des geschreibenen AIF |
| AIF_DATEN | binary | AIF Hex-Daten |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG AIF lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG AIF lesen |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-selbsttest-starten"></a>
### SELBSTTEST_STARTEN

Starten des Selbsttests KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_NR | int | gewaehltes Testscript 0 - standard tests, &gt; 0 nur für Entwicklung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-selbsttest-stoppen"></a>
### SELBSTTEST_STOPPEN

Abbrechen des Selbsttests KWP2000: $32 StopRoutineByLocalIdentifier $04 Selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-selbsttest-abfragen"></a>
### SELBSTTEST_ABFRAGEN

Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $04 Selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_TESTERG_NR | unsigned int | Status des Tests 0x00: 	Test nicht gestartet 0x01: 	Test laeuft 0x7F: 	Test abgebrochen 0x81: 	Test beendet mit Fehler 0xFF: 	Test beendet ohne Fehler |
| ID_TESTERG_TEXT | string | Teststatus-Text table Testergebnisse TESTERG_TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemtest-starten"></a>
### SYSTEMTEST_STARTEN

Starten des Systemtests KWP2000: $31 StartRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_NR | unsigned int | gewaehltes Testscript 0 - standard tests, &gt; 0 nur für Entwicklung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemtest-stoppen"></a>
### SYSTEMTEST_STOPPEN

Abbrechen des Systemtests KWP2000: $32 StopRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemtest-abfragen"></a>
### SYSTEMTEST_ABFRAGEN

Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $FA OEM-spezifisch: Systemtest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_TESTERG_NR | unsigned int | Status des Tests 0x00: 	Test nicht gestartet 0x01: 	Test laeuft 0x7F: 	Test abgebrochen 0x81: 	Test beendet mit Fehler 0xFF: 	Test beendet ohne Fehler |
| ID_TESTERG_TEXT | string | Teststatus-Text table Testergebnisse TESTERG_TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-logistic-nr"></a>
### READ_LOGISTIC_NR

Auslesen der Logistiknummer KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| LOGISTIC_NO | string | BMW Logistic Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-wa-code"></a>
### READ_WA_CODE

WA-Code auslesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| WA_CODE | string | WA-Code |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-ende-codierung"></a>
### SET_ENDE_CODIERUNG

Codierdaten flashen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-logistic-nr"></a>
### SET_LOGISTIC_NR

Modify Logistic Nr KWP2000: $2E WriteDataByCommonIdentifier Dieser job schickt zusaetzlich ein set_ende_codierung Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOGISTIC_NO | string | BMW Logistic Nummer (12 digits) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ser-nr-dom-lesen"></a>
### SER_NR_DOM_LESEN

Seriennummer 14-stellig lesen KWP2000: $21 ReadDataByLocalIdentifier $E0 Local ID SER_NR_DOM Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SER_NR_DOM | string | Seriennummer Geraet (14-stellig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-blocklaenge"></a>
### SCHREIBEN_BLOCKLAENGE

max. Blocklaenge zum SW-Laden KWP2000: $2e WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROTOKOLL_VERSION | string | Protokol Version: XXL oder Standard table ProtVersionTABLE Prot_Version |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-current-uif"></a>
### READ_CURRENT_UIF

currentUIFDataTable KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| UIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| UIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| UIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| UIF_OFFSET | int | Anzahl Programmiervorgaenge |
| UIF_GROESSE | int | Groesse des UIF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-bmw-sach-nr"></a>
### READ_BMW_SACH_NR

SystemSupplierECUHardwareNumber KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_HW_NR | string | BMW-Hardwarenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-bmw-hw-version"></a>
### READ_BMW_HW_VERSION

vehicleManufactureECUHardwareVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_HW_NR | string | BMW-HardwareVersion |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-program-referenz-lesen"></a>
### PROGRAM_REFERENZ_LESEN

vehicleManufECUSoftwareLayerVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PROGRAMM_REFERENZ | string | PRGREF ProgrammReferenz letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-display"></a>
### STATUS_DISPLAY

Info ueber die aktuell verwendeten Displays KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS |
| STAT_DISPLAY_WIDTH | int | Breite des Display |
| STAT_DISPLAY_HIGHT | int | Hoehe des Display |
| STAT_BITS_PER_PIXEL | int | Bit/Pixel |
| STAT_LOOKUP_TABL_SIZE | long | Size Color Lookup table |
| STAT_COLOR_MODELL | int | TEST_STATUS |
| STAT_COLOR_FORMAT | int | TEST_STATUS |
| STAT_DISPLAY_MEMORY_AVAIL | long | TEST_STATUS |
| STAT_GENERIC_FLAGS | string | TEST_STATUS |
| STAT_GENERIC_FLAGS_TEXT | string | TEST_STATUS |
| STAT_NUM_DISPLAY | int | TEST_STATUS |
| STAT_REFRESH_RATE | int | TEST_STATUS |
| STAT_MONITOR_TYPE | int | TEST_STATUS |
| STAT_DISPLAY_FLAGS | string | Anzahl der Displays |
| STAT_DISPLAY_FLAGS_TEXT | string | Anzahl der Displays |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-memory-usage"></a>
### STATUS_MEMORY_USAGE

Aktueller Verbrauch der System Recourcen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS |
| STAT_RAM_USED_WERT | int | RAM in use (%) |
| STAT_RAM_USED_EINH | string | Einheit RAM_EINH |
| STAT_ROM_USED_WERT | int | ROM in use (%) |
| STAT_ROM_USED_EINH | string | Einheit ROM |
| STAT_FLASHFS_USED_WERT | int | aktuelle Groesse FileSystem in use (%) |
| STAT_FLASHFS_USED_EINH | string | Einheit Groesse FileSystem |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-memory-available"></a>
### STATUS_MEMORY_AVAILABLE

Groesse der verfuegbaren System Recourcen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS |
| STAT_RAM_AVAIL_WERT | unsigned long | RAM verfuegbar (BYTE) |
| STAT_RAM_AVAIL_EINH | string | Einheit RAM |
| STAT_ROM_AVAIL_WERT | unsigned long | ROM verfuegbar (BYTE) |
| STAT_ROM_AVAIL_EINH | string | Einheit ROM |
| STAT_FLASHFS_AVAIL_WERT | unsigned long | aktuelle Groesse FileSystem verfuegbar (BYTE) |
| STAT_FLASHFS_AVAIL_EINH | string | aktuelle Groesse FileSystem verfuegbar (BYTE) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dvd-temperature"></a>
### STATUS_DVD_TEMPERATURE

Status der Temperatur des DVD Laufwerks KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS |
| STAT_TEMP_WERT | int | aktuelle temperatur |
| STAT_TEMP_EINH | string | Einheit STAT_TEMP_WERT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drive-dvd"></a>
### STATUS_DRIVE_DVD

Status des DVD-Laufwerks wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS |
| STAT_PLAYER_MODE | unsigned int | Laufwerks Modus table DriveModeTABLE WERT |
| STAT_PLAYER_MODE_TEXT | string | Laufwerks Modus table DriveModeTABLE STATUS_TEXT |
| STAT_PLAYER_COMMENT | unsigned int | Laufwerks Modus Kommentar table DriveModeCommentTABLE WERT |
| STAT_PLAYER_COMMENT_TEXT | string | Laufwerks Modus Kommentar table DriveModeCommentTABLE STATUS_TEXT |
| STAT_LOADER | unsigned int | Laufwerks Ladezustand table DriveLoadingStateTABLE WERT |
| STAT_LOADER_TEXT | string | Laufwerks Ladezustand table DriveLoadingStateTABLE STATUS_TEXT |
| STAT_LOADER_COMMENT | unsigned int | Kommentar zum Ladezustand table DriveLoadingCommentTABLE WERT |
| STAT_LOADER_COMMENT_TEXT | string | Kommentar zum Ladezustand table DriveLoadingCommentTABLE STATUS_TEXT |
| STAT_MEDIUM | unsigned int | Medium table DriveMediumTABLE WERT |
| STAT_MEDIUM_TEXT | string | Medium table DriveMediumTABLE STATUS_TEXT |
| STAT_MEDIUM_STATE | unsigned int | aktuelle Medium Zustand table DriveMediumStateTABLE WERT |
| STAT_MEDIUM_STATE_TEXT | string | aktuelle Medium Zustand table DriveMediumStateTABLE STATUS_TEXT |
| STAT_EJECT_LOCK | unsigned int | Eject moeglich oder blockiert table DriveEjectStateTABLE WERT |
| STAT_EJECT_LOCK_TEXT | string | Eject moeglich oder blockiert table DriveEjectStateTABLE STATUS_TEXT |
| STAT_THERMAL_STATE | unsigned int | aktueller Temperatur Zustand table DriveThermalStateTABLE WERT |
| STAT_THERMAL_STATE_TEXT | string | aktueller Temperatur Zustand table DriveThermalStateTABLE STATUS_TEXT |
| STAT_POWER | unsigned int | aktueller Power Zustand table DrivePowerStateTABLE WERT |
| STAT_POWER_TEXT | string | aktueller Power Zustand table DrivePowerStateTABLE STATUS_TEXT |
| STAT_ERROR | unsigned int | Fehler Zustand table DriveErrorTABLE WERT |
| STAT_ERROR_TEXT | string | Fehler Zustand table DriveErrorTABLE STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drive-cd"></a>
### STATUS_DRIVE_CD

Status des CD-Laufwerks wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS |
| STAT_PLAYER_MODE | unsigned int | Laufwerks Modus table DriveModeTABLE WERT |
| STAT_PLAYER_MODE_TEXT | string | Laufwerks Modus table DriveModeTABLE STATUS_TEXT |
| STAT_PLAYER_COMMENT | unsigned int | Laufwerks Modus Kommentar table DriveModeCommentTABLE WERT |
| STAT_PLAYER_COMMENT_TEXT | string | Laufwerks Modus Kommentar table DriveModeCommentTABLE STATUS_TEXT |
| STAT_LOADER | unsigned int | Laufwerks Ladezustand table DriveLoadingStateTABLE WERT |
| STAT_LOADER_TEXT | string | Laufwerks Ladezustand table DriveLoadingStateTABLE STATUS_TEXT |
| STAT_LOADER_COMMENT | unsigned int | Kommentar zum Ladezustand table DriveLoadingCommentTABLE WERT |
| STAT_LOADER_COMMENT_TEXT | string | Kommentar zum Ladezustand table DriveLoadingCommentTABLE STATUS_TEXT |
| STAT_MEDIUM | unsigned int | Medium table DriveMediumTABLE WERT |
| STAT_MEDIUM_TEXT | string | Medium table DriveMediumTABLE STATUS_TEXT |
| STAT_MEDIUM_STATE | unsigned int | aktuelle Medium Zustand table DriveMediumStateTABLE WERT |
| STAT_MEDIUM_STATE_TEXT | string | aktuelle Medium Zustand table DriveMediumStateTABLE STATUS_TEXT |
| STAT_EJECT_LOCK | unsigned int | Eject moeglich oder blockiert table DriveEjectStateTABLE WERT |
| STAT_EJECT_LOCK_TEXT | string | Eject moeglich oder blockiert table DriveEjectStateTABLE STATUS_TEXT |
| STAT_THERMAL_STATE | unsigned int | aktueller Temperatur Zustand table DriveThermalStateTABLE WERT |
| STAT_THERMAL_STATE_TEXT | string | aktueller Temperatur Zustand table DriveThermalStateTABLE STATUS_TEXT |
| STAT_POWER | unsigned int | aktueller Power Zustand table DrivePowerStateTABLE WERT |
| STAT_POWER_TEXT | string | aktueller Power Zustand table DrivePowerStateTABLE STATUS_TEXT |
| STAT_ERROR | unsigned int | Fehler Zustand table DriveErrorTABLE WERT |
| STAT_ERROR_TEXT | string | Fehler Zustand table DriveErrorTABLE STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-taster"></a>
### STATUS_TASTER

Status aller Taster wird ausgegeben Die Daten koennen nur dann zurueckgeben werden, wenn der CCC in Zustand 'FIB ist aktuell' ist (s. JOB status_fib_create) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS table HostSTATETABLE ANZEIGE_TEXT |
| STAT_DVD_AUSWURF | string | Button DVD Auswurf Status: pressed/released table ButtonStateTABLE STATUS_TEXT |
| STAT_CD_AUSWURF | string | Button CD Auswurf Status: pressed/released table ButtonStateTABLE STATUS_TEXT |
| STAT_VORWAERTS | string | Button CD vorwaerts Status: pressed/released table ButtonStateTABLE STATUS_TEXT |
| STAT_RUECKWAERTS | string | Button CD rueckwaerts Status: pressed/released table ButtonStateTABLE STATUS_TEXT |
| STAT_DREHKNOPF | string | Button Lautstaerke Status: pressed/released table ButtonStateTABLE STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drehknopf"></a>
### STATUS_DREHKNOPF

Der aktuelle Status des Drehknopfs wird ausgegeben Die Daten können nur dann zurueckgeben werden, wenn der CCC in Zustand 'FIB ist aktuell' ist (s. JOB status_fib_create) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | string | TEST_STATUS table HostSTATETABLE ANZEIGE_TEXT |
| STAT_DREHPOSITION | long | aktuelle Position des Drehknopfes |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cd-swl"></a>
### STATUS_CD_SWL

Der aktuelle SWL-Status bei SWL von CD wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CCC_SWL | int | Total CCC SW-Loading status |
| STAT_CCC_SWL_TEXT | string | Total CCC SW-Loading status table SwlStatusAllTABLE STATUS_TEXT |
| STAT_NO_CPUS | int | number of ECUs in response |
| STAT_ECU_ID | int | EcuId |
| STAT_PER_CENT_COMPLETE | int | completion percentage |
| STAT_ECU_UPDATE | int | SW-Loading status |
| STAT_ECU_UPDATE_TEXT | string | SW-Loading status table SwlStatusTABLE STATUS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-end-swl"></a>
### SET_END_SWL

Schließe Most-Lade-Prozedur ab KWP2000: $31 StartFunctionByLocalId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-generate-fib"></a>
### GENERATE_FIB

Erstelle neues FastBootImage KWP2000: $31 StartFunctionByLocalId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fib-create"></a>
### STATUS_FIB_CREATE

aktueller Zustand des FastBootImage KWP2000: $33 GetRoutineResultByLocalId Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FIBTESTZEIT | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FIB_CREATE | int | 1E: FIB wird generiert, 1F: FIB ist aktuell |
| STAT_FIB_CREATE_TEXT | string | OKAY, wenn fehlerfrei table FibStatusTABLE STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eject-cd"></a>
### STEUERN_EJECT_CD

Falls eine CD im Laufwerk ist, wird sie ausgeworfen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eject-dvd"></a>
### STEUERN_EJECT_DVD

Falls ein Medium im DVD Laufwerk ist, wird es ausgeworfen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-laufwerk"></a>
### STATUS_LESEN_LAUFWERK

Auslesen des codierten Laufwerks (CD Laufwerk oder MD Laufwerk) KWP2000: $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAUFWERK | int | Codiertes Laufwerk table DriveTable WERT |
| STAT_LAUFWERK_TEXT | string | Codiertes Laufwerk table DriveTable ANZEIGE_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-internal-reset"></a>
### STEUERN_INTERNAL_RESET

Seuergeraete reset ausloesen KWP2000: $11 ECUReset $FA RequestInternalReset Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (32 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (1 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (22 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (9 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (33 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (38 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (9 × 9)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (3 × 3)
- [FWINERROR](#table-fwinerror) (1 × 3)
- [IADDRESSE](#table-iaddresse) (1 × 5)
- [TESTERGEBNISSE](#table-testergebnisse) (5 × 2)
- [HOSTSTATETABLE](#table-hoststatetable) (5 × 2)
- [DISPLAYFLAGS](#table-displayflags) (4 × 2)
- [SWLSTATUSTABLE](#table-swlstatustable) (45 × 2)
- [SWLSTATUSALLTABLE](#table-swlstatusalltable) (5 × 2)
- [FIBSTATUSTABLE](#table-fibstatustable) (4 × 2)
- [INFOLOGFILETABLE](#table-infologfiletable) (35 × 2)
- [CDSTATUSTABLE](#table-cdstatustable) (2 × 2)
- [ECUIDTABLE](#table-ecuidtable) (6 × 2)
- [DRIVEMODETABLE](#table-drivemodetable) (7 × 2)
- [DRIVEMODECOMMENTTABLE](#table-drivemodecommenttable) (16 × 2)
- [DRIVELOADINGSTATETABLE](#table-driveloadingstatetable) (7 × 2)
- [DRIVELOADINGCOMMENTTABLE](#table-driveloadingcommenttable) (4 × 2)
- [DRIVEMEDIUMTABLE](#table-drivemediumtable) (4 × 2)
- [DRIVEMEDIUMSTATETABLE](#table-drivemediumstatetable) (10 × 2)
- [DRIVEEJECTSTATETABLE](#table-driveejectstatetable) (3 × 2)
- [DRIVETHERMALSTATETABLE](#table-drivethermalstatetable) (9 × 2)
- [DRIVEPOWERSTATETABLE](#table-drivepowerstatetable) (9 × 2)
- [DRIVEERRORTABLE](#table-driveerrortable) (7 × 2)
- [BUTTONSTATETABLE](#table-buttonstatetable) (3 × 2)
- [PROTVERSIONTABLE](#table-protversiontable) (3 × 2)
- [DRIVETABLE](#table-drivetable) (3 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

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

Dimensions: 72 rows × 2 columns

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
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 32 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xE1CC | Ein Device hat eine Monitor Nachricht nicht bekommen oder beantwortet (Error_Monitoring). |
| 0xE1CD | Gesamtring konnte nicht aufgestartet werden (Error_WakeUp_Failed). |
| 0xE1CE | Obwohl Shutdown(Execute) geschickt wurde ging das Licht nicht aus. (Error_Light_Not_Off). |
| 0xE1CF | Die zentrale Registry ist fehlerhaft (Error_Registry_New). |
| 0xE1D0 | Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose). |
| 0xE1D1 | Lange und/oder haeufige Unlocks (Error_Unlock_Long). |
| 0xE1D2 | Shutdown wegen Uebertemperatur (Error_Tempshutdown). |
| 0xA3CE | CD Services nicht Verfuegbar |
| 0xA3CF | CD Laufwerk steht im Reset |
| 0xA3D0 | CD Laufwerk Kommunikationsfehler |
| 0xA3D1 | Keine Verbindung zwischen Companion Chip und CAN-Transceiver |
| 0xA3D2 | Keine Verbindung zwischen Companion Chip und I/O-Expander |
| 0xA3D3 | Keine Verbindung zwischen Companion Chip und MOST |
| 0xA3D4 | Keine CAN Verbindung zum Tuner |
| 0xA3D5 | Keine CAN Verbindung zum ASK |
| 0xA3D6 | Keine CAN Verbindung zum LVDS |
| 0xA3D7 | Keine UART Verbindung zum Nav |
| 0xA3D8 | Keine CAN Verbindung zum hinteren LVDS |
| 0xA3D9 | DVD Services nicht Verfuegbar |
| 0xA3DA | DVD Laufwerk steht im Reset |
| 0xA3DB | DVD Laufwerk Kommunikationsfehler |
| 0xA3DC | Ungueltige FIB Checksumme |
| 0xA3DD | Keine Verbindung I2S Speech Out - DSP (ASK) -Speech In |
| 0xA3DE | Video In defect (obsolete) |
| 0xA3DF | Abweichung zwischen SH4-Clock und RealTime-Clock |
| 0xA3E0 | Abweichung zwischen PCI-Clock und RealTime-Clock |
| 0xA3E1 | Defekte im SDRAM |
| 0xA3E2 | Defekte im externen SDRAM |
| 0xA3E3 | Defekte im NAND-Flash |
| 0xA3E4 | FlashFileSystem konnte nicht gestartet werden |
| 0xA3E5 | Keine IPC-Verbindung zum Gateway |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00000000 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 1 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 22 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xE1CC | 0x20 | 0x21 | 0x05 | - |
| 0xE1CD | 0x20 | 0x21 | - | - |
| 0xE1CE | 0x20 | 0x21 | - | - |
| 0xE1CF | 0x20 | 0x21 | 0x05 | - |
| 0xE1D0 | 0x20 | 0x21 | 0x06 | - |
| 0xE1D1 | 0x20 | 0x21 | - | - |
| 0xE1D2 | 0x20 | 0x21 | - | - |
| 0xA3CE | 0x20 | 0x21 | - | - |
| 0xA3CF | 0x20 | 0x21 | - | - |
| 0xA3D0 | 0x20 | 0x21 | - | - |
| 0xA3D4 | 0x20 | 0x21 | - | - |
| 0xA3D5 | 0x20 | 0x21 | - | - |
| 0xA3D6 | 0x20 | 0x21 | - | - |
| 0xA3D7 | 0x20 | 0x21 | - | - |
| 0xA3D8 | 0x20 | 0x21 | - | - |
| 0xA3D9 | 0x20 | 0x21 | - | - |
| 0xA3DA | 0x20 | 0x21 | - | - |
| 0xA3DB | 0x20 | 0x21 | - | - |
| 0xA3DC | 0x20 | 0x21 | - | - |
| 0xA3DD | 0x20 | 0x21 | - | - |
| 0xA3DE | 0x20 | 0x21 | - | - |
| default | 0x20 | 0x21 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x05 | Diagnoseadresse | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | NPR | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x07 | Uebertemperatur | Grad C | - | unsigned long | - | 1 | 1 | 0 |
| 0x10 | Logische-Knotenadresse | Hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x11 | FBlockID | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x12 | InstID | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x13 | FktID | Hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x20 | VDOError | Hex | - | unsigned long | - | 1 | 1 | 0 |
| 0x21 | Datenlaenge | Hex | - | unsigned char | - | 1 | 1 | 0 |

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
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 33 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | Device bekam Reset (Error_Reset). |
| 0x9309 | Bis zum Auftreten des Timeouts konnte kein Licht bzw. kein stabiler Lock erkannt werden (Error_NSInit_Timeout). |
| 0x930A | Device ist im Zustand Normal Operation und das Licht am Eingang geht ohne Vorankuendigung aus (Error_Sudden_light_off). |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist (Error_Device_No_Answer). |
| 0x930C | Kurze Unlocks (Error_unlock_Short). |
| 0x930D | Kein Broadcast Configuration.Status vom Networkmaster erhalten (Error_t_CfgStatus). |
| 0x930F | Ein Device hat im laufenden Betrieb seinen Bypass All geschlossen (Error_NCE). |
| 0x9310 | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK). |
| 0x9408 | Abweichung SH4 clock von der real time clock. |
| 0x9409 | Abweichung PCI clock von der real time clock. |
| 0x940A | Defekte im internen SDRAM. |
| 0x940B | Defekte im externen SDRAM. |
| 0x940C | Defekte im NAND flash. |
| 0x940D | Video In defekt (Chip 7118 antwortet nicht). |
| 0xA3C8 | Checksum Error |
| 0xA3C9 | Illegaler Speicher Zugriff |
| 0xA3CA | Illegaler Resourcen Zugriff |
| 0xA3CB | Timelimit Exeeded |
| 0xA3CC | Detected Software Exception |
| 0xA3CD | OS-Fehler |
| 0xA3CE | CD/MD Drive errors (obsolete) |
| 0xA3CF | DVD Drive errors (obsolete) |
| 0xA3D0 | No CAN connection to Tuner (obsolete) |
| 0xA3D1 | No CAN connection to ASK (obsolete) |
| 0xA3D2 | No CAN Connection to LVDS (obsolete) |
| 0xA3D3 | No connection UART to Nav (obsolete) |
| 0xA3D4 | No CAN Connection to Rear Seat LVDS (obsolete) |
| 0xA3D5 | No connection between companion chip and CAN transceiver (obsolete) |
| 0xA3D6 | No connection between companion chip and I/O expander (obsolete) |
| 0xA3D7 | No connection companion chip to Video Out (obsolete) |
| 0xA3DD | Wrong FIB checksum (obsolete) |
| 0xA3DF | No Connection I2S Speech Out - DSP (ASK) -Speech In (obsolete) |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 10000000 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 38 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9308 | 0x20 | 0x21 | - | - |
| 0x9309 | 0x20 | 0x21 | - | - |
| 0x930A | 0x20 | 0x21 | - | - |
| 0x930B | 0x20 | 0x21 | iAddresse | - |
| 0x930C | 0x20 | 0x21 | - | - |
| 0x930D | 0x20 | 0x21 | - | - |
| 0x930F | 0x20 | 0x21 | 0x05 | - |
| 0x9310 | 0x20 | 0x21 | iAddresse | - |
| 0x9408 | 0x20 | 0x21 | iAddresse | - |
| 0x9409 | 0x20 | 0x21 | iAddresse | - |
| 0x940A | 0x20 | 0x21 | iAddresse | - |
| 0x940B | 0x20 | 0x21 | iAddresse | - |
| 0x940C | 0x20 | 0x21 | iAddresse | - |
| 0x940D | 0x20 | 0x21 | iAddresse | - |
| 0xA3C8 | 0x20 | 0x21 | - | - |
| 0xA3C9 | 0x20 | 0x21 | - | - |
| 0xA3CA | 0x20 | 0x21 | - | - |
| 0xA3CB | 0x20 | 0x21 | - | - |
| 0xA3CC | 0x20 | 0x21 | - | - |
| 0xA3CD | 0x20 | 0x21 | - | - |
| 0xA3CE | 0x20 | 0x21 | - | - |
| 0xA3CF | 0x20 | 0x21 | - | - |
| 0xA3D0 | 0x20 | 0x21 | - | - |
| 0xA3D1 | 0x20 | 0x21 | - | - |
| 0xA3D2 | 0x20 | 0x21 | - | - |
| 0xA3D3 | 0x20 | 0x21 | - | - |
| 0xA3D4 | 0x20 | 0x21 | - | - |
| 0xA3D5 | 0x20 | 0x21 | - | - |
| 0xA3D6 | 0x20 | 0x21 | - | - |
| 0xA3D7 | 0x20 | 0x21 | - | - |
| 0xA3D8 | 0x20 | 0x21 | - | - |
| 0xA3D9 | 0x20 | 0x21 | - | - |
| 0xA3DA | 0x20 | 0x21 | - | - |
| 0xA3DB | 0x20 | 0x21 | - | - |
| 0xA3DC | 0x20 | 0x21 | - | - |
| 0xA3DD | 0x20 | 0x21 | - | - |
| 0xA3DF | 0x20 | 0x21 | - | - |
| default | 0x20 | 0x21 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | TaskId | Hex | - | signed char | - | 1 | 1 | 0 |
| 0x05 | Diagnoseadresse | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x10 | Logische-Knotenadresse | Hex | - | unsigned int | - | 1 | 1 | 0 |
| 0x11 | FBlockID | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x12 | InstID | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x13 | FktID | Hex | - | unsigned int | - | 1 | 1 | 0 |
| 0x20 | VDOError | Hex | - | unsigned long | - | 1 | 1 | 0 |
| 0x21 | DatenLaenge | Hex | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 3 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 0xxxxxxx | 00 | unused |
| 1xxxxxxx | 01 | unused |
| xxxxxxxx | 1 | unused |

<a id="table-fwinerror"></a>
### FWINERROR

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW_1 | UW_2 |
| --- | --- | --- |
| 2 | 20 | 21 |

<a id="table-iaddresse"></a>
### IADDRESSE

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x10 | 0x11 | 0x12 | 0x13 |

<a id="table-testergebnisse"></a>
### TESTERGEBNISSE

Dimensions: 5 rows × 2 columns

| TESTERG_NR | TESTERG_TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft - Nummer  |
| 0x7F | Test abgebrochen |
| 0x81 | Test beendet mit Fehler  |
| 0xFF | Test beendet |

<a id="table-hoststatetable"></a>
### HOSTSTATETABLE

Dimensions: 5 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Status OK |
| 0x01 | Could not retrieve data |
| 0x02 | Ausgabe Puffer zu klein! |
| 0x03 | Daten noch nicht verfuegbar! |
| 0xXY | nicht definiert |

<a id="table-displayflags"></a>
### DISPLAYFLAGS

Dimensions: 4 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x01 | True color system |
| 0x02 | Indexed color system |
| 0x04 | Monochrome mode |
| 0x08 | Gray scale mode |

<a id="table-swlstatustable"></a>
### SWLSTATUSTABLE

Dimensions: 45 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | ECU_DOWNLOAD_IN_PROGRESS |
| 0x01 | ECU_DONE |
| 0x02 | ECU_TO_BE_UPDATED |
| 0xD6 | ECU_ERROR_TFFS_EXTRACTION |
| 0xD7 | ECU_ERROR_TFFS_CREATION |
| 0xD8 | ECU_ERROR_RAMDISK_CREATION |
| 0xD9 | ECU_ERROR_UNKNOWN_OVERALL_STATUS |
| 0xDA | ECU_ERROR_CD_VERSION_TOO_BIG |
| 0xDB | ECU_ERROR_VERSION_CHECKSUM_MISMATCH |
| 0xDC | ECU_ERROR_NO_PROJMAPPING |
| 0xDD | ECU_ERROR_NO_HWMAPPING |
| 0xDE | ECU_ERROR_INVALID_FAST_IMAGE |
| 0xDF | ECU_ERROR_NO_ECU_RESPONSE |
| 0xE0 | ECU_ERROR_ILLEGAL_PROG_TYPE |
| 0xE1 | ECU_ERROR_READING_HIP_VERS |
| 0xE2 | ECU_ERROR_CHECKSUM_MISMATCH |
| 0xE3 | ECU_ERROR_INVALID_IMAGE_HEADER |
| 0xE4 | ECU_ERROR_PROCESSING_VERSION_FILE |
| 0xE5 | ECU_WARNING_LINE_NOT_OF_INTEREST |
| 0xE6 | ECU_WARNING_COULD_NOT_UPDATE_AIF |
| 0xE7 | ECU_ERROR_NO_ECUS |
| 0xE8 | ECU_ERROR_DISC_CHANGE |
| 0xE9 | ECU_ERROR_LABEL_NOT_FOUND |
| 0xEA | ECU_ERROR_SECTION_DATA |
| 0xEB | ECU_ERROR_SECTION_PROG |
| 0xEC | ECU_ERROR_CANT_OPEN_FILE |
| 0xED | ECU_ERROR_IMAGEIO |
| 0xEE | ECU_ERROR_WRONG_SOURCE |
| 0xEF | ECU_ERROR_WRITING_FILE |
| 0xF0 | ECU_ERROR_READING_FILE |
| 0xF1 | ECU_WARNING_UNKNOWN_COMMAND |
| 0xF2 | ECU_ERROR_UNKNOWN_SCRIPT |
| 0xF3 | ECU_ERROR_READING_KWP |
| 0xF4 | ECU_ERROR_SRIPT_PARSING |
| 0xF5 | ECU_ERROR_INFOLOG_READ |
| 0xF6 | ECU_ERROR_UNKNOWN_BOOTMODE |
| 0xF7 | ECU_ERROR_FILESIZE_MISMATCH |
| 0xF8 | ECU_ERROR_TOO_MANY_ECUS |
| 0xF9 | ECU_ERROR_DISC_INSERTED |
| 0xFA | ECU_ERROR_DISC_EJECTED |
| 0xFB | ECU_ERROR_PROCESSING_SCRIPT |
| 0xFC | ECU_ERROR_NOT_ENOUGH_MEMORY  |
| 0xFD | ECU_ERROR_IMAGE_NOT_FOUND |
| 0xFE | ECU_ERROR_SCRIPT_NOT_FOUND  |
| 0xff | unknown status |

<a id="table-swlstatusalltable"></a>
### SWLSTATUSALLTABLE

Dimensions: 5 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | CCC SW-Laden aktiv |
| 0x01 | CCC SW-Laden abgeschlossen oder nicht gestartet |
| 0x02 | Fehler |
| 0x03 | Erfolgreich und CD noch im Laufwerk |
| 0xff | unknown status |

<a id="table-fibstatustable"></a>
### FIBSTATUSTABLE

Dimensions: 4 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x1E | FIB wird erstellt |
| 0x1F | FIB ist aktuell |
| 0x12 | FIB ist nicht aktuell |
| 0xff | unknown status |

<a id="table-infologfiletable"></a>
### INFOLOGFILETABLE

Dimensions: 35 rows × 2 columns

| WERT | FILE_NAME |
| --- | --- |
| 0x01 | ProdStamp |
| 0x02 | PlatDef |
| 0x03 | DebugMessage |
| 0x04 | TSW_ErrorArray |
| 0x08 | Most |
| 0x09 | PortParameter |
| 0x10 | BootMode |
| 0x11 | TswMode |
| 0x12 | Trm |
| 0x20 | SWload |
| 0x21 | SwConfig |
| 0x22 | SWLDiag |
| 0x25 | BWMSachNrHist |
| 0x30 | ResetData |
| 0x31 | SWLFragment |
| 0x32 | SWLStatus |
| 0x40 | Diagnosis |
| 0x41 | DiagTestArray |
| 0x60 | Host_EcuData |
| 0x61 | Appl_EcuData |
| 0x62 | Host_DataErrLog |
| 0x63 | Appl_DataErrLog |
| 0x64 | CfgErrLog |
| 0x65 | CfgDServ |
| 0x80 | CD_Data |
| 0x90 | Display_Setup |
| 0x91 | DownloadProcessInfo |
| 0x92 | DownloadStatusInfo |
| 0x93 | Dvd_Video_Service_Data |
| 0x100 | TSW |
| 0x102 | TestArray |
| 0x200 | ADC |
| 0x201 | TrimediaTst |
| 0x220 | BrowserCodierdaten |
| 0xFFFF | all |

<a id="table-cdstatustable"></a>
### CDSTATUSTABLE

Dimensions: 2 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | no SWL CD in drive |
| 0x01 | SWL CD in drive |

<a id="table-ecuidtable"></a>
### ECUIDTABLE

Dimensions: 6 rows × 2 columns

| WERT | ECU_TEXT |
| --- | --- |
| 0x3F | Enhanced Audio |
| 0x47 | Tuner |
| 0x62 | Gateway |
| 0x63 | Host |
| 0xA0 | Application |
| 0xXY | unknown |

<a id="table-drivemodetable"></a>
### DRIVEMODETABLE

Dimensions: 7 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Kein Medium im Laufwerk erfolgreich analysiert |
| 0x01 | Player im Stop Mode |
| 0x02 | Player spielt Musik |
| 0x03 | Player im Pause Mode |
| 0x04 | Player schneller Vorlauf |
| 0x05 | Player schneller Ruecklauf |
| 0xXY | unknown |

<a id="table-drivemodecommenttable"></a>
### DRIVEMODECOMMENTTABLE

Dimensions: 16 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Laufwerk ist READY |
| 0x01 | Ergebnis eines Benutzerkommandos |
| 0x02 | Neues Medium eingelegt |
| 0x03 | Ende des Mediums |
| 0x04 | Start des Mediums |
| 0x05 | Ende der Spur |
| 0x10 | Laufwerk ist nicht READY |
| 0x11 | Laufwerk ist tot |
| 0x12 | Medium konnte nicht erkannt werden |
| 0x13 | Laufwerks Temperatur zu hoch |
| 0x14 | Laufwerk hat keine externe Clock |
| 0x15 | Inst. Ext. clock recovery fehlgeschlagen |
| 0x16 | Externe Clock verfuegbar |
| 0x17 | Neues Medium, aber keine externe Clock |
| 0x18 | Medium wird analysiert |
| 0xXY | unknown |

<a id="table-driveloadingstatetable"></a>
### DRIVELOADINGSTATETABLE

Dimensions: 7 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Kein Medium im Laufwerk |
| 0x01 | Disc wird eingelegt |
| 0x02 | Disc wird ausgeworfen |
| 0x03 | Disc ist ausgeworfen |
| 0x04 | Disc ist im Laufwerk |
| 0x05 | Unbekannte Disc Position |
| 0xXY | unknown |

<a id="table-driveloadingcommenttable"></a>
### DRIVELOADINGCOMMENTTABLE

Dimensions: 4 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | kein Kommentar |
| 0x01 | Ladezustand auf Aufforderung geaendert |
| 0x11 | Laufwerk ist tot |
| 0xXY | unknown |

<a id="table-drivemediumtable"></a>
### DRIVEMEDIUMTABLE

Dimensions: 4 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Medium Typ unbekannt |
| 0x01 | Medium im Laufwerk ist eine CD |
| 0x02 | Medium im Laufwerk ist eine DVD  |
| 0xXY | unknown |

<a id="table-drivemediumstatetable"></a>
### DRIVEMEDIUMSTATETABLE

Dimensions: 10 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Medium unbekannt |
| 0x01 | Daten detektiert, ISO 9660 Filesystem verfuegbar |
| 0x02 | CDDA detektiert |
| 0x03 | SuperAudio CD detektiert |
| 0x04 | Video CD |
| 0x05 | Super Video CD |
| 0x06 | DVD video |
| 0x07 | DVD audio |
| 0x08 | DVD daten & video mixed mode Medium |
| 0xXY | unknown |

<a id="table-driveejectstatetable"></a>
### DRIVEEJECTSTATETABLE

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Software blockiert Eject Button nicht |
| 0x01 | Software blockiert Eject Button |
| 0xXY | unknown |

<a id="table-drivethermalstatetable"></a>
### DRIVETHERMALSTATETABLE

Dimensions: 9 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Temperatur zu niedrig (FATAL) |
| 0x01 | Temperatur zu niedrig (CRITICAL) |
| 0x02 | Temperatur niedrig |
| 0x03 | Temperatur normal |
| 0x04 | Temperatur hoch |
| 0x05 | Temperatur zu hoch (CRITICAL) |
| 0x06 | Temperatur zu hoch (FATAL) |
| 0xFF | Temperatur nicht definiert |
| 0xXY | unknown |

<a id="table-drivepowerstatetable"></a>
### DRIVEPOWERSTATETABLE

Dimensions: 9 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Spannung nicht OK (FATAL) |
| 0x01 | Spannung sehr niedrig (CRITICAL) |
| 0x02 | Spannung niedrig |
| 0x03 | Spannung normal |
| 0x04 | Spannung hoch |
| 0x05 | Spannung sehr hoch (CRITICAL) |
| 0x06 | Spannung zu hoch (FATAL) |
| 0xFF | Spannung noch nicht verfuegbar |
| 0xXY | unknown |

<a id="table-driveerrortable"></a>
### DRIVEERRORTABLE

Dimensions: 7 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Keine weiteren Fehlerfaelle |
| 0x01 | Disc wurde analysiert, ist aber nicht lesbar |
| 0x02 | Temperatur Problem |
| 0x04 | Spannungsversorgung nicht OK |
| 0x08 | External Clock Fehler |
| 0x10 | Keine Kommunikation mit dem Laufwerk moeglich |
| 0xXY | unknown |

<a id="table-buttonstatetable"></a>
### BUTTONSTATETABLE

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x01 | released |
| 0x00 | pressed |
| 0xXY | unknown |

<a id="table-protversiontable"></a>
### PROTVERSIONTABLE

Dimensions: 3 rows × 2 columns

| WERT | PROT_VERSION |
| --- | --- |
| 0x00FA | Standard |
| 0x037A | XXL |
| 0xXY | unknown |

<a id="table-drivetable"></a>
### DRIVETABLE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x04 | CD_LAUFWERK |
| 0x05 | MD_LAUFWERK |
| 0xXY | unknown |
