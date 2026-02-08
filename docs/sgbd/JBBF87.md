# JBBF87.prg

- Jobs: [91](#jobs)
- Tables: [33](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | JBBF |
| ORIGIN | BMW EI-61 Sefik Uzun |
| REVISION | 9.000 |
| AUTHOR | Lear Entwicklung Arseni Martínez, Lear Entwicklung Carme Tàpias, Lear Entwicklung Israel Revert |
| COMMENT | SGBD of JBBFE for E8x E9x (C-Sample) |
| PACKAGE | 1.29 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [READ_ADDRCODINGDEFAULT](#job-read-addrcodingdefault) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $21 ReadDataByLocalIdentifier $7D RecordLocalId
- [CLEAR_ADDRCODINGDEFAULT](#job-clear-addrcodingdefault) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $7D RecordLocalId
- [CLEAR_DTC_MEMORY](#job-clear-dtc-memory) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $7E RecordLocalId
- [AIF_LESEN_READECU](#job-aif-lesen-readecu) - Auslesen des Anwender Informations Feldes KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default
- [READ_ENERGY_SAVING_MODE](#job-read-energy-saving-mode) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Inputs $01 ReportCurrentState
- [STATUS_DIGITAL_OUTPUTS](#job-status-digital-outputs) - Auslesen der Stati von den digitalen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Outputs $01 ReportCurrentState
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Inputs $01 ReportCurrentState
- [STATUS_ANALOG_OUTPUTS](#job-status-analog-outputs) - Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Outputs $01 ReportCurrentState
- [STATUS_SENSE_INPUTS](#job-status-sense-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Sense Inputs $01 ReportCurrentState
- [STATUS_INTERNAL_VARIABLES](#job-status-internal-variables) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState
- [STEUERN_DIGITAL_INPUT](#job-steuern-digital-input) - Digitale Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $07 ShortTermAdjustment
- [STEUERN_DIGITAL_OUTPUT](#job-steuern-digital-output) - Digitale Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Ouput $07 ShortTermAdjustment
- [STEUERN_ANALOG_INPUT](#job-steuern-analog-input) - Analoge Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Input $07 ShortTermAdjustment
- [STEUERN_ANALOG_OUTPUT](#job-steuern-analog-output) - Analoge Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Output $07 ShortTermAdjustment
- [STEUERN_SENSE_INPUT](#job-steuern-sense-input) - Diagnostic Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $05 Digitale Input $07 ShortTermAdjustment
- [STEUERN_BEENDEN](#job-steuern-beenden) - Kontrolle an JBBFE zurueckgeben KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $02 Digitale Output $03 Analoge Input $04 Analoge Output $05 Sense Input $00 ReturnControToECU
- [_FS_LESEN_LEAR](#job-fs-lesen-lear) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [KOMPRESSOR_PARAMETERS_WRITE](#job-kompressor-parameters-write) - Schreiben die kompressor parameters KWP2000: $3B WriteDataByLocalIdentifier $7C RecordLocalId
- [KOMPRESSOR_PARAMETERS_READ](#job-kompressor-parameters-read) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $21 ReadDataByLocalIdentifier $7C RecordLocalId
- [FUELTANK_PARAMETERS_RESET](#job-fueltank-parameters-reset) - Schreiben die fullstand parameters KWP2000: $3B WriteDataByLocalIdentifier $7B RecordLocalId
- [FUELTANK_PARAMETERS_READ](#job-fueltank-parameters-read) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $21 ReadDataByLocalIdentifier $7B RecordLocalId
- [READ_L4969_REGISTERS](#job-read-l4969-registers) - Schreiben die fullstand parameters KWP2000: $21 ReadDataByLocalIdentifier $7A RecordLocalId
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_1](#job-status-historienspeicher-lesen-block-1) - EnergieDatenSpeicher Teil 1 -Einschlafverhinderer- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE1 commonProjectSpecific
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_2](#job-status-historienspeicher-lesen-block-2) - EnergieDatenSpeicher Teil 2 -Wecker- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific
- [STEUERN_HISTORIENSPEICHER_LOESCHEN](#job-steuern-historienspeicher-loeschen) - EnergieDatenSpeicher Teil 1 und TEIL 2 loeschen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE0 commonProjectSpecific
- [STATUS_VERSION_GATEWAYMODULES](#job-status-version-gatewaymodules) - Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6F RecordLocalId Modus  : Default
- [SLEEP_MODE_FUNKTIONAL](#job-sleep-mode-funktional) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default
- [STEUERN_FENSTERHEBER_EINLERNEN](#job-steuern-fensterheber-einlernen) - Init apinch through diagnosis KWP2000: $22   ReadDataByCommonIdentifier $0001 project specific. Init apinch
- [STATUS_FENSTERHEBER](#job-status-fensterheber) - Init apinch through diagnosis KWP2000: $22   ReadDataByCommonIdentifier $0004 project specific. Status apinch
- [STEUERN_FENSTERHEBER_DENORMIEREN](#job-steuern-fensterheber-denormieren) - Init apinch through diagnosis KWP2000: $22   ReadDataByCommonIdentifier $0005 project specific. Init apinch
- [STEUERN_FENSTERHEBER_HINTEN](#job-steuern-fensterheber-hinten) - Rear windows direkte ansteuern Ohne EKS, direkte Ausgang Steuerung Mit EKS, Steuerung ändernde Eingang und durch Application KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Ouput $07 ShortTermAdjustment
- [READ_VARIANT](#job-read-variant) - Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6E RecordLocalId Modus  : Default
- [_JBBFE_CONFIGURATION](#job-jbbfe-configuration) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $7A RecordLocalId
- [STATUS_FH_LOG](#job-status-fh-log) - Ursachen der letzten Unnormalisierung des Fensters KWP2000: $22   ReadDataByCommonIdentifier $0008 project specific. Status Fensters
- [_CHECK_DTC_MEMO](#job-check-dtc-memo) - Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6D RecordLocalId Modus  : Default
- [FS_LOESCHEN_SELEKTIV](#job-fs-loeschen-selektiv) - Fehlerspeicher loeschen Selektiv KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [_LEAR_SLEEP_MODE](#job-lear-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $FA LearPowerDown Modus  : Default
- [STEUERN_WASCHDUESE_AUSSENSPIEGEL](#job-steuern-waschduese-aussenspiegel) - Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $79 RecordLocalId
- [STATUS_FH_POSITION](#job-status-fh-position) - Lesen der FH position KWP2000: $21 ReadDataByLocalIdentifier $79 RecordLocalId
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $78 RecordLocalId
- [STEUERN_ZWP](#job-steuern-zwp) - Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $77 RecordLocalId

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

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

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

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
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | unsigned int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTHG_TEXT |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
| FLASH_SCHREIBEN_ANZAHL | unsigned int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
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
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-read-addrcodingdefault"></a>
### READ_ADDRCODINGDEFAULT

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $21 ReadDataByLocalIdentifier $7D RecordLocalId

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clear-addrcodingdefault"></a>
### CLEAR_ADDRCODINGDEFAULT

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $7D RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | soll 0 sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clear-dtc-memory"></a>
### CLEAR_DTC_MEMORY

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $7E RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | soll 0 sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-lesen-readecu"></a>
### AIF_LESEN_READECU

Auslesen des Anwender Informations Feldes KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-saving-mode"></a>
### READ_ENERGY_SAVING_MODE

Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ENERGY_SAVING_MODE | string | Ausgabe des Engery-Saving-Modes table EnergySaving NAME TEXT |
| STAT_PROD_MODE | int | 0: Produktionsmode nicht aktiv 1: Produktionsmode aktiv |
| STAT_TRA_MODE | int | 0: Transportmode nicht aktiv 1: Transportmode aktiv |
| STAT_HO_MODE | int | 0: Werkstattmode nicht aktiv 1: Werkstattmode aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Inputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHIFTREGISTER_DATA_EIN | int | Shift Register Data 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 7,PORT P6.6 |
| STAT_AUCSENSOR_EIN | int | AUC Sensor Eingang. PWM Signal 0: NICHT AKTIV, 1: AKTIV Wert am Pin umgekehrt! Actual value inverted! PIN 23, PORT P7.4 |
| STAT_FH_FATH_GESCHW_SENSOR1_EIN | int | Fensterheber Fahrer hinten Geschwindigkeitsensor 1 0: Geschlossen, 1: Offen PowerWindow RearDriver SpeedSensor 1 0: Closed, 1: Open PIN 48, PORT P2.1 |
| STAT_FH_FATH_GESCHW_SENSOR2_EIN | int | Fensterheber Fahrer hinten Geschwindigkeitsensor 2 0: Geschlossen, 1: Offen PowerWindow RearDriver SpeedSensor 2 0: Closed, 1: Open PIN 49, PORT P2.2 |
| STAT_FH_BFTH_GESCHW_SENSOR1_EIN | int | Fensterheber Beifahrer hinten Geschwindigkeitsensor 1 0: Geschlossen, 1: Offen PowerWindow RearPassenger SpeedSensor 1 0: Closed, 1: Open PIN 50, PORT P2.3 |
| STAT_FH_BFTH_GESCHW_SENSOR2_EIN | int | Fensterheber Beifahrer hinten Geschwindigkeitsensor 2 0: Geschlossen, 1: Offen PowerWindow RearPassenger SpeedSensor 2 0: Closed, 1: Open PIN 51, PORT P2.4 |
| STAT_SERIALCOM_VR_IN_EIN | int | Voltage-Regulator Serial-Communication Input 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 54, PORT P2.7 |
| STAT_PTWAKE_EIN | int | PT-CAN Wake-up Eingang 0: NICHT AKTIV, 1: AKTIV Wert am Pin umgekehrt! Actual Value Inverted! PIN 58, PORT P2.9 |
| STAT_HECKKLAPPE_TASTER_EIN | int | Taster Entriegeln Heckklappe (Interrupt) 0: Keine Betätigung, 1: Taster Gedrückt Trunklid External Switch (Interrupt) 0: Not pushed, 1: Pushed Wert am Pin umgekehrt! Actual Value Inverted! PIN 60, PORT P2.11 |
| STAT_HECKSCHEIBE_TASTER_EIN | int | Taster Entriegeln Heckscheibe (Interrupt) 0: Keine Betätigung, 1: Taster Gedrückt RearWindow External Switch (Interrupt) 0: Not pushed, 1: Pushed Wert am Pin umgekehrt! Actual Value Inverted! PIN 61, PORT P2.12 |
| STAT_HECKKLAPPE_KONTAKT_EIN | int | Heckklappe Kontakt 0: Geschlossen, 1: Offen Trunklid Contact 0: Closed, 1: Open PIN 62, PORT P2.13 |
| STAT_HECKSCHEIBE_KONTAKT_EIN | int | Heckscheibe Kontakt 0: Geschlossen, 1: Offen RearWindow Contact 0: Closed, 1: Open PIN 63, PORT P2.14 |
| STAT_VOLTAGEREGULATOR_INT_EIN | int | Voltage-Regulator Interrupt Input 0: AKTIV (Low), 1: NICHT AKTIV (High) Internes Signal der JBBF Not External JBBF Input PIN 64, PORT P2.15 |
| STAT_SPI_INPUT_EIN | int | EEPROM. Serial-Communication Input 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 75, PORT P3.8 |
| STAT_RX_DIAG_EIN | int | External Serial-Communication Input 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 78, PORT P3.11 |
| STAT_FH_WAKECONTROL_EIN | int | Fenterheber Aufwachen Steuerung PowerWindow Wake Control 0: OFF, 1: ON PIN 81,PORT P3.15 |
| STAT_LOWSPEEDCAN_RX_EIN | int | K-CAN Transceiver. Serial-Communication Input 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 89, PORT P4.4 |
| STAT_HIGHSPEEDCAN_RX_EIN | int | PT-CAN Transceiver. Serial-Communication Input 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 90, PORT P4.5 |
| STAT_EMU_MODE_EIN | int | EMU Mode 0: ON, 1: OFF Internes Signal der JBBF Not External JBBF Input PIN 100, PORT P0L.0 |
| STAT_ADAPT_MODE_EIN | int | Adapt Mode 0: ON, 1: OFF Internes Signal der JBBF Not External JBBF Input PIN 101,PORT P0L.1 |
| STAT_EN_BOOT_LOAD_EIN | int | Enable Bootmode Load 0: ON, 1: OFF Internes Signal der JBBF Not External JBBF Input PIN 104,PORT P0L.4 |
| STAT_CHIPSELECTLINE1_EIN | int | Chip Select Line 1 Internes Signal der JBBF Not External JBBF Input PIN 111,PORT P0H.1 |
| STAT_CHIPSELECTLINE2_EIN | int | Chip Select Line 2 Internes Signal der JBBF Not External JBBF Input PIN 112,PORT P0H.2 |
| STAT_CHIPSELECTLINE_EIN | string | Chip Select Line Value 0: 3 CS lines, 1: 2 CS lines, 2: Not CS lines, 3: 5 CS lines Internes Signal der JBBF Not External JBBF Input Internal Configuration InputS |
| STAT_SEGMENT_ADDR_LINE_SELECT3_EIN | int | Segment Address Line Select 3 Internes Signal der JBBF Not External JBBF Input PIN 113,PORT P0H.3 |
| STAT_SEGMENT_ADDR_LINE_SELECT4_EIN | int | Segment Address Line Select 4 Internes Signal der JBBF Not External JBBF Input PIN 114,PORT P0H.4 |
| STAT_SEGMENT_ADDR_LINE_SELECT_EIN | string | Segment Address Lines 0: 4-bit Segment Addr, 1: Not Segment Addr, 2: 8-bit, 3: 2-bit Internes Signal der JBBF Not External JBBF Input Internal Configuration Inputs |
| STAT_CLKCFG5_EIN | int | Clock Configuration 5 Internes Signal der JBBF Not External JBBF Input PIN 115,PORT P0H.5 |
| STAT_CLKCFG6_EIN | int | Clock Configuration 6 Internes Signal der JBBF Not External JBBF Input PIN 116,PORT P0H.6 |
| STAT_CLKCFG7_EIN | int | Clock Configuration 7 Internes Signal der JBBF Not External JBBF Input PIN 117,PORT P0H.7 |
| STAT_CLKCFG_EIN | string | Multiplier Factor (Fcpu=FxtalxF) 0: Fxtal x2.5, 1: x0.5, 2: x1.5, 3: x1, 4: x5, 5: x2, 6: x3, 7: x4 Internes Signal der JBBF Not External JBBF Input Internal Configuration Inputs |
| STAT_FRONTWISCHER_RSK_EIN | int | Frontwischer Rückstellkontakt 0: FrontWischer nicht im RSK, 1: FrontWischer im RSK Front Wiper Park Position 0: Wiper Not in Park Position, 1: Wiper in Park Position Wert am Pin umgekehrt! Actual Value Inverted! ShiftRegisterSwitch.1 |
| STAT_HECKWISCHER_RSK_EIN | int | Heckwischer Rückstellkontakt 0: HeckWischer nicht im RSK, 1: HeckWischer im RSK Rear Wiper Park Position 0: Wiper Not in Park Position, 1: Wiper in Park Position Wert am Pin umgekehrt! Actual Value Inverted! ShiftRegisterSwitch.2 |
| STAT_DSC_BEFEHL_EIN | int | DSC Taster 0: Keine Betätigung, 1:Taster Gedrückt DSC Switch 0: Not Pushed, 1: Pushed Wert am Pin umgekehrt! Actual Value Inverted! ShiftRegisterSwitch.3 |
| STAT_KUEHLMITTELSTAND_EIN | int | Kühlmittelstand 0: Zu niedriger Füllstand, 1: Normaler Füllstand Cooling Level Sensor 0: Under Level, 1: Over Level Wert am Pin umgekehrt! Actual Value Inverted! ShiftRegisterSwitch.5 |
| STAT_WASCHWASSERSTAND_EIN | int | Waschwasserstand 0: Zu niedriger Füllstand, 1: Normaler Füllstand Water Level Sensor 0: Under Level, 1: Over Level Wert am Pin umgekehrt! Actual Value Inverted! ShiftRegisterSwitch.6 |
| STAT_HANDBREMSE_KONTAKT_EIN | int | Handbremsekontakt 0: Gelöst, 1: Angezogen Handbrake Switch Input 0: Not Active, 1: Active Wert am Pin umgekehrt! Actual Value Inverted! ShiftRegisterSwitch.7 |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-outputs"></a>
### STATUS_DIGITAL_OUTPUTS

Auslesen der Stati von den digitalen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Outputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUCSENSOR_ENABLE_EIN | int | AUC-Sensor befähigen AUC-Sensor Enable 0: Disable, 1: Enable PIN 1,PORT P6.0 |
| STAT_EEPROM_ENABLE_EIN | int | EEprom Enable 0: Enable, 1: Disable Internes Signal der JBBF Not External JBBF Input PIN 2,PORT P6.1 |
| STAT_KL30SW_ENABLE_EIN | int | KL30SW befähigen KL30SW Enable 0: Disable, 1: Enable PIN 3,PORT P6.2 |
| STAT_5V_SENSOR_ENABLE_EIN | int | 5V SENSOR befähigen 5V SENSOR Enable 0: Disable, 1: Enable PIN 4,PORT P6.3 |
| STAT_SHIFTREGISTER_CONTROL_EIN | int | Shift Register Control 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 5,PORT P6.4 |
| STAT_SHIFTREGISTER_CLOCK_EIN | int | Shift Register Clock 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 6,PORT P6.5 |
| STAT_FRONTWASCHERPUMPE_EIN | int | Front Wascher Pumpe 0: Aus, 1: Ein Front Washer Pump 0: OFF, 1: ON PIN 10,PORT P8.1 |
| STAT_HECKWASCHERPUMPE_EIN | int | Heck Wascher Pumpe 0: Aus, 1: Ein Rear Washer Pump 0: OFF, 1: ON PIN 12,PORT P8.3 |
| STAT_SONNENROLLO_LOWTREIBER1_EIN | int | SunBlind Mosfet LowSide  1 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 13,PORT P8.4 |
| STAT_SONNENROLLO_HIGHTREIBER1_EIN | int | SunBlind Mosfet HighSide 1 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 14,PORT P8.5 |
| STAT_SONNENROLLO_LOWTREIBER2_EIN | int | SunBlind Mosfet LowSide  2 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 15,PORT P8.6 |
| STAT_SONNENROLLO_HIGHTREIBER2_EIN | int | SunBlind Mosfet HighSide 2 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 16,PORT P8.7 |
| STAT_SONNENROLLO_AUSGANG_EIN | int | Sonnenrollo 0: Aus, 5: Von Ein zu Aus, 6: Nach oben, 9: Herunter Sunblind Output 0: OFF, 5: ON2OFF, 6: UP, 9: DOWN |
| STAT_TANKSENSOREN_ENABLE_EIN | int | FuelTank Sensoren befähigen Fuel Tank Enable 0: DISABLE, 1: ENABLE PIN 24,PORT P7.5 |
| STAT_SERIALCOM_VR_OUT_EIN | int | Data Out to Voltage Regulator 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 52,PORT P2.5 |
| STAT_SERIALCOM_VR_CLOCK_EIN | int | Clock Out to Voltage Regulator 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 53,PORT P2.6 |
| STAT_CONTACTWAKE_IN_ENABLE_EIN | int | Contacts Wake Enable 0: Disable, 1: Enable Internes Signal der JBBF Not External JBBF Input PIN 57,PORT P2.8 |
| STAT_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_RECHTS_EIN | int | Waschdüsenheizung und Aussenspiegel rechts JetWasher Heating Right 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 70,PORT P3.5 |
| STAT_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_LINKS_EIN | int | Waschdüsenheizung und Aussenspiegel links JetWasher Heating Left 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 73,PORT P3.6 |
| STAT_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_AUSGANG_EIN | int | Waschdüsenheizung und Aussenspiegel Jet Washer Heater Output 0: Aus, 1: Rechts ein, 2: Links ein, 3: Beides ein 0: OFF, 1: RIGHT, 2: LEFT, 3: ON |
| STAT_PTWAKE_OUT_EIN | int | PT CAN Wake UP Pulse 0: NICHT AKTIV, 1: AKTIV 0: NOT ACTIVE, 1: ACTIVE PIN 74,PORT P3.7 |
| STAT_SPI_OUTPUT_EIN | int | SPI Data Out 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 76,PORT P3.9 |
| STAT_TX_DIAG_EIN | int | Diagnostic TX (Serial Channel) 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 77,PORT P3.10 |
| STAT_SPI_CLOCK_EIN | int | SPI Data Clock 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 80,PORT P3.13 |
| STAT_ZUSATZWASSERPUMPE_EIN | int | Zusatzwasserpumpe 0: Aus, 1: Ein Additional Water Pump 0: OFF, 1: ON PIN 86,PORT P4.1 |
| STAT_FH_CHIPSELECT_EIN | int | PowerWindow Chip Select 0: Disable, 1: Enable Internes Signal der JBBF Not External JBBF Input PIN 87,PORT P4.2 |
| STAT_HIGHSPEEDCAN_ENABLE_EIN | int | High Speed CAN Enable 0: Enable, 1: Disable Internes Signal der JBBF Not External JBBF Input PIN 88,PORT P4.3 |
| STAT_HIGHSPEEDCAN_TX_EIN | int | High Speed CAN TX 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 91,PORT P4.6 |
| STAT_LOWSPEEDCAN_TX_EIN | int | Low Speed CAN TX 0: LOW, 1: HIGH Internes Signal der JBBF Not External JBBF Input PIN 92,PORT P4.7 |
| STAT_FH_BFTH_AUF_EIN | int | Fensterheber Beifahrer Hinten Auf (Relaissteuerung) PowerWindow RearPassenger OPENRELAY 0: OFF, 1: ON PIN 118,PORT P1L.0 |
| STAT_FH_BFTH_ZU_EIN | int | Fensterheber Beifahrer Hinten Zu (Relaissteuerung) PowerWindow RearPassenger CLOSERELAY 0: OFF, 1: ON PIN 119,PORT P1L.1 |
| STAT_FH_BFTH_AUSGANG_EIN | int | Fensterheber Beifahrer Hinten (Relaissteuerung) 0: Aus, 1: Auf, 2: Zu PowerWindow RearPassenger Output 0: OFF, 1: DOWN, 2: UP |
| STAT_FH_FATH_ZU_EIN | int | Fensterheber Fahrer Hinten Auf (Relaissteuerung) PowerWindow RearDriver OPENRELAY 0: OFF, 1: ON PIN 120,PORT P1L.2 |
| STAT_FH_FATH_AUF_EIN | int | Fensterheber Fahrer Hinten Zu (Relaissteuerung) PowerWindow RearDriver CLOSERELAY 0: OFF, 1: ON PIN 121,PORT P1L.3 |
| STAT_FH_FATH_AUSGANG_EIN | int | Fensterheber Fahrer Hinten (Relaissteuerung) 0: Aus, 1: Auf, 2: Zu PowerWindow RearDriver Output 0: OFF, 1: DOWN, 2: UP |
| STAT_HECKWISCHER_EIN | int | Heckwischer (Relaissteuerung) 0: Aus, 1: Ein RearWiper Relay 0: OFF, 1: ON PIN 122,PORT P1L.4 |
| STAT_FRONTWISCHER_EIN | int | Frontwischer Ein/Aus (Relaissteuerung) 0: Aus, 1: Ein FrontWiper Relay 0: OFF, 1: ON PIN 123,PORT P1L.5 |
| STAT_FRONTWISCHER_GESCHW_EIN | int | Frontwischer Geschwingdigkeit (Relaissteuerung) FrontWiper Speed Relay 0: OFF, 1: ON PIN 124,PORT P1L.6 |
| STAT_FRONTWISCHER_AUSGANG_EIN | int | Frontwischer (Relaissteuerung) 0: Aus, 1: Stufe 1, 3: Stufe 2 FrontWiper Output 0: OFF, 1: STATE1, 3: STATE2 |
| STAT_SRA_EIN | int | Scheinwerferreinigungsanlage (Relaissteuerung) 0: Aus, 1: Ein HeadLamp Washer Relay 0: OFF, 1: ON PIN 125,PORT P1L.7 |
| STAT_ZV_SICHERN_RELAIS_EIN | int | Zentralverriegelung Sichernrelais CentralLocking SECURERELAY 0: OFF, 1: ON PIN 128,PORT P1H.0 |
| STAT_ZV_ENTRIEGELN_RELAIS_EIN | int | Zentralverriegelung Entriegelnrelais CentralLocking UNLOCKRELAY 0: OFF, 1: ON PIN 129,PORT P1H.1 |
| STAT_ZV_VERRIEGELN_RELAIS_EIN | int | Zentralverriegelung Verriegelnrelais CentralLocking LOCKRELAY 0: OFF, 1: ON PIN 130,PORT P1H.2 |
| STAT_ZV_SELEKTIV_ENTRIEGELN_RELAIS_EIN | int | Zentralverriegelung selektiv Entriegelnrelais CentralLocking LOCKDRIVERRELAY 0: OFF, 1: ON PIN 131,PORT P1H.3 |
| STAT_ZV_AUSGANG_EIN | int | Zentralverriegelung 0: Aus, 2: Entriegeln, 6: Selektiv Entriegeln, 12: Verriegeln, 13: Sichern, 14: Entsichern CentralLocking Output 0: OFF, 2: ER, 6: SER, 12: VR, 13: VRZS, 14: ES |
| STAT_HECKKLAPPE_EIN | int | Heckklappe (Relaissteuerung) 0: Aus, 1: Ein TrunkLid Relay 0: OFF, 1: ON PIN 132,PORT P1H.4 |
| STAT_HECKSCHEIBE_EIN | int | Heckscheibe (Relaissteuerung) 0: Aus, 1: Ein RearWindow Relay 0: OFF, 1: ON PIN 133,PORT P1H.5 |
| STAT_HECKSCHEIBENHEIZUNG_EIN | int | Heckscheibenheizung (Relaissteuerung) 0: Aus, 1: Ein RearWindow Heater Relay 0: OFF, 1: ON PIN 134,PORT P1H.6 |
| STAT_BISTABILRELAIS_ON_EIN | int | Biestabiles Relais ON 0: Aus, 1: Ein Biestable Relay On 0: OFF, 1: ON PIN 135,PORT P1H.7 |
| STAT_BISTABILRELAIS_OFF_EIN | int | Biestabiles Relais OFF 0: Aus, 1: Ein Biestable Relay On 0: OFF, 1: ON Wert am Pin umgekehrt! Actual Value Inverted! PIN 85,PORT P4.0 |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-inputs"></a>
### STATUS_ANALOG_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Inputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_KOMPRESSORVENTIL_STROM_WERT | int | Digital Wandler Wert von Kompressor Ventil Strom Digital converted value from Compressor Current Sensor Wertbereich: 0..0x3FF (1023) PIN 27,PORT P5.0 |
| STAT_ADC_DRUCKSENSOR_WERT | int | Digital Wandler Wert von Druck Sensor Digital converted value from Pressure Sensor (HEX) Wertbereich: 0..0x3FF (1023),Gültig:0x052(82)..0x3AD(941) PIN 28,PORT P5.1 |
| STAT_DRUCKSENSOR_WERT | real | Druck Sensor Pressure Sensor (P)[bar] Wertebereich: -3.34&lt;-&gt;38.34,Gültig:0..35 [bar] P=(((HEX)-0.4*(1023/5))*35)/859, for Vref=5V PIN 28,PORT P5.1 |
| STAT_DRUCKSENSOR_EINH | string | Einheit fuer Druck: bar |
| STAT_ADC_FH_BFT_SCHALTER_WERT | int | Digital Wandler Wert von Fensterheber Beifahrer Schalter Digital converted value from PowerWindow Passenger Button Wertbereich: 0..0x3FF(1023) 143(0x08F)....346(0x15A) : DOWNAUTO(2) 347(0x15B)....571(0x23B) : DOWNMANUAL(1) 572(0x23C)....756(0x2F4) : UPAUTO(4) 757(0x2F5)....951(0x3B7) : UPMANUAL(3) 952(0x3B8)....1023(0x3FF): OFF(0) PIN 29,PORT P5.2 |
| STAT_VAR_FH_BFT_SCHALTER | int | Fensterheber Beifahrer Schalter 0: Keine Betätigung, 1: Manuell-Öffnen, 2: Maut-Öffnen, 3: Manuell-Schließen, 4: Maut-Schließen PowerWindow Passenger Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO PIN 29,PORT P5.2 |
| STAT_FH_BFT_SCHALTER_TEXT | string | Fensterheber Beifahrer Schalter Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 PowerWindow Passenger Button OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 PIN 29,PORT P5.2 |
| STAT_ADC_FH_FATH_SCHALTER_WERT | int | Digital Wandler Wert von Fensterheber Fahrer Hinten Schalter Digital converted value from PowerWindow Rear-Driver Button Wertbereich: 0..0x3FF(1023) 143(0x08F)....346(0x15A) : DOWNAUTO(2) 347(0x15B)....571(0x23B) : DOWNMANUAL(1) 572(0x23C)....756(0x2F4) : UPAUTO(4) 757(0x2F5)....951(0x3B7) : UPMANUAL(3) 952(0x3B8)....1023(0x3FF): OFF(0) PIN 30,PORT P5.3 |
| STAT_VAR_FH_FATH_SCHALTER | int | Fensterheber Fahrer Hinten Schalter 0: Keine Betätigung, 1: Manuell-Öffnen, 2: Maut-Öffnen, 3: Manuell-Schließen, 4: Maut-Schließen PowerWindow Rear-Driver Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO PIN 30,PORT P5.3 |
| STAT_FH_FATH_SCHALTER_TEXT | string | Fensterheber Fahrer Hinten Schalter Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 PowerWindow Rear-Driver Button OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 PIN 30,PORT P5.3 |
| STAT_ADC_FH_BFTH_SCHALTER_WERT | int | Digital Wandler Wert von Fensterheber Beifahrer Hinten Schalter Digital converted value from PowerWindow Rear-Passenger Button Wertbereich: 0..0x3FF(1023) 143(0x08F)....346(0x15A) : DOWNAUTO(2) 347(0x15B)....571(0x23B) : DOWNMANUAL(1) 572(0x23C)....756(0x2F4) : UPAUTO(4) 757(0x2F5)....951(0x3B7) : UPMANUAL(3) 952(0x3B8)....1023(0x3FF): OFF(0) PIN 31,PORT P5.4 |
| STAT_VAR_FH_BFTH_SCHALTER | int | Fensterheber Beifahrer Hinten Schalter 0: Keine Betätigung, 1: Manuell-Öffnen, 2: Maut-Öffnen, 3: Manuell-Schließen, 4: Maut-Schließen PowerWindow Rear-Passenger Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO PIN 31,PORT P5.4 |
| STAT_FH_BFTH_SCHALTER_TEXT | string | Fensterheber Beifahrer Hinten Schalter Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 PowerWindow Rear-Passenger Button OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 PIN 31,PORT P5.4 |
| STAT_ADC_TANK_FA_FUELLSTAND_WERT | int | Digital Wandler Wert von Fuel Tank Fahrer (1) Digital converted value from Fuel Tank Driver (1) Wertbereich: 0..0x3FF(1023) PIN 32,PORT P5.5 |
| STAT_TANK_FA_WIDERSTAND_WERT | real | Widerstand Fuel Tank Fahrer (1) Resistance Fuel Tank Driver (1) Wertebereich: Gültig: 0..1207 [Ohm], 0xFFFF Signal ungültig PIN 32,PORT P5.5 |
| STAT_TANK_FA_WIDERSTAND_EINH | string | Einheit fuer Widerstand Fuel Tank: Ohm |
| STAT_ADC_TANK_BF_FUELLSTAND_WERT | int | Digital Wandler Wert von Fuel Tank Beifahrer (2) Digital converted value from Fuel Tank Passenger (2) (HEX) Wertbereich: 0..0x3FF(1023) PIN 33,PORT P5.6 |
| STAT_TANK_BF_WIDERSTAND_WERT | real | Widerstand Fuel Tank Beifahrer (2) Resistance Fuel Tank Passenger (2) Wertebereich: Gültig: 0..1207 [Ohm], 0xFFFF Signal ungültig PIN 33,PORT P5.6 |
| STAT_TANK_BF_WIDERSTAND_EINH | string | Einheit fuer Widerstand Fuel Tank: Ohm |
| STAT_ADC_FH_BFTH_STROM_WERT | int | Digital Wandler Wert von Fensterheber Beifahrer Hinten Strom Digital converted value from PowerWindow Rear-Passenger Current (HEX) Wertbereich: 0..0x3FF (1023) PIN 34,PORT P5.7 |
| STAT_FH_BFTH_STROM_WERT | real | Strom Fensterheber Beifahrer Hinten Current PowerWindow Rear-Passenger Wertbereich: 0 A..39 A (PH)=((HEX)*39)/1024  [A] for Vref=5V PIN 34,PORT P5.7 |
| STAT_FH_BFTH_STROM_EINH | string | Einheit fuer Current PowerWindow Rear-Passenger: Amp |
| STAT_ADC_FH_FATH_STROM_WERT | int | Digital Wandler Wert von Fensterheber Fahrer Hinten Strom Digital converted value from PowerWindow Rear-Driver Current (HEX) Wertbereich: 0..0x3FF (1023) PIN 35,PORT P5.8 |
| STAT_FH_FATH_STROM_WERT | real | Strom Fensterheber Fahrer Hinten Current PowerWindow Rear-Driver Wertbereich: 0..39 [A] (PH)=((HEX)*39)/1024  [A] for Vref=5V PIN 35,PORT P5.8 |
| STAT_FH_FATH_STROM_EINH | string | Einheit fuer Current PowerWindow Rear-Driver: Amp |
| STAT_ADC_FONDSCHICHTUNGSENSOR_WERT | int | Digital Wandler Wert von Fondschichtung Sensor Digital converted value from Rear Air Flow Sensor (HEX) Wertbereich: 0..0x3FF (1023),Gültig:0x133(307)..0x2B8(696) PIN 36,PORT P5.9 |
| STAT_FONDSCHICHTUNGSENSOR_WERT | real | Schichtung Fondschichtung Sensor [%] Opening Rear Air Flow Sensor Wertebereich: -85.51&lt;-&gt;184,Gültig:0..100 [%] (PH)=(((HEX)-1.5*(1023/5))*100)/389, for Vref=5V PIN 36,PORT P5.9 |
| STAT_FONDSCHICHTUNGSENSOR_EINH | string | Einheit fuer Fondschichtung: % |
| STAT_ADC_SONNENROLLO_STROM_WERT | int | Digital Wandler Wert von Sonnenrollo Strom Sensor Digital converted value from Sonnenrollo Strom Sensor Wertbereich: 0..0x3FF (1023) PIN 39,PORT P5.10 |
| STAT_SONNENROLLO_STROM_WERT | real | Sonnenrollo Strom Sensor Wertebereich: 0..12 [A] (PH)=12.2775*HEX/1024, for Vref=5V PIN 39,PORT P5.10 |
| STAT_SONNENROLLO_STROM_EINH | string | Einheit fuer Druck: Amp |
| STAT_ADC_BATTERIE_SPANNUNG_WERT | int | Digital Wandler Wert von Batterie Spannung Sensor Digital converted value from Battery Voltage Sensor (HEX) Wertbereich: 0..0x3FF (1023) PIN 40,PORT P5.11 |
| STAT_BATTERIE_SPANNUNG_WERT | real | Batterie Spannung Battery Voltage (Vbat) [V] Wertbereich: 0..28.40 [V] Vbat=(HEX)*100/3605, for Vref=5V PIN 40,PORT P5.11 |
| STAT_BATTERIE_SPANNUNG_EINH | string | Einheit fuer Batterie Spannung: Volt |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-outputs"></a>
### STATUS_ANALOG_OUTPUTS

Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Outputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KOMPRESSORVENTIL_EIN | int | Compressor Valve Control 0: ON, 1: OFF PIN 19,PORT P7.0 |
| STAT_KOMPRESSORVENTIL_PWM_WERT | int | Spannung Compressor Valve Control PWM Wertbereich: 0..0xFFFF (65535),Gültig:0..0x061B (1563)--&gt;0%..100% |
| STAT_PROZENT_KOMPRESSORVENTIL_PWM_WERT | real | Spannung Kompressor Ventil PWM [%] Wertbereich: 0..0xFFFF (65535),Gültig:0..0x061B (1563)--&gt;0%..100% (PH)=(1563-HEX)*100/1563, for Vref=5V |
| STAT_PROZENT_KOMPRESSORVENTIL_PWM_EINH | string | Einheit fuer KompressorVentil: % |
| STAT_WASSERVENTIL_EIN | int | Water Valve Control 0: ON, 1: OFF PIN 20,PORT P7.1 |
| STAT_WASSERVENTIL_PWM_WERT | int | Spannung Water Valve Control PWM Wertbereich: 0..0xFFFF (65535),Gültig:0..0x0168 (360)--&gt;0%..100% |
| STAT_PROZENT_WASSERVENTIL_PWM_WERT | real | Spannung Wasser Ventil PWM [%] Wertbereich: 0..0xFFFF (65535),Gültig:0..0x0168 (360)--&gt;0%..100% (PH)=(HEX)*10/36, for Vref=5V |
| STAT_PROZENT_WASSERVENTIL_PWM_EINH | string | Einheit fuer WasserVentil: % |
| STAT_SITZHEIZUNG_FA_EIN | int | SeatHeating Driver Control 0: ON, 1: OFF PIN 21,PORT P7.2 |
| STAT_ADC_SITZHEIZUNG_FA_PWM_WERT | unsigned int | Spannung SeatHeating Driver Control PWM Wertbereich: 0..0xFFFF (65535) |
| STAT_SITZHEIZUNG_FA_PWM_WERT | string | Spannung SeatHeating Driver Control PWM 25000: OFF, 20000: STATE1, 12500: STATE2, 7500: STATE3 |
| STAT_SITZHEIZUNG_BF_EIN | int | SeatHeating Passenger Control 0: ON, 1: OFF PIN 22,PORT P7.3 |
| STAT_ADC_SITZHEIZUNG_BF_PWM_WERT | unsigned int | Spannung SeatHeating Passenger Control PWM Wertbereich: 0..0xFFFF (65535) |
| STAT_SITZHEIZUNG_BF_PWM_WERT | string | Spannung SeatHeating Passenger Control PWM 25000: OFF, 20000: STATE1, 12500: STATE2, 7500: STATE3 |
| STAT_EINH | string | Einheit fuer alle Analogwerte: Volt |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-inputs"></a>
### STATUS_SENSE_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Sense Inputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FIVEVOLTS_SENSOR_DIAG_WERT | int | Digital Wandler Wert von FiveVoltsSensor Diag Wertbereich: 0..0x3FF (1023) PIN 41,PORT P5.12 |
| STAT_SPANNUNG_FIVEVOLTS_SENSOR_DIAG_WERT | real | Spannung FiveVolts Sensor Voltage FiveVolts Sensor [V] Wertebereich: 0&lt;-&gt;16 [V],Gültig: 4.7..5.3 [V] V=HEX/64 [V], for Vref=5V PIN 41,PORT P5.12 |
| STAT_SPANNUNG_FIVEVOLTS_SENSOR_DIAG_EINH | string | Einheit fuer Spannung FiveVolts Sensor: Volt |
| STAT_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_DIAG_WERT | int | Digital Wandler Wert von JetWasherHeating Diag Wertbereich: 0..0x3FF (1023) PIN 42,PORT P5.13 |
| STAT_STROM_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_DIAG_WERT | real | JetWasherHeating Diag Wertebereich: 0..12 [A] (PH)=12.2775*HEX/1024, for Vref=5V PIN 42,PORT P5.13 |
| STAT_STROM_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_DIAG_EINH | string | Einheit fuer JetWasherHeating: Amp |
| STAT_WASCHERPUMPE_DIAG_WERT | int | Digital Wandler Wert von Wascherpumpe Diag Wertbereich: 0..0x3FF (1023) PIN 43,PORT P5.14 |
| STAT_WASSERVENTIL_DIAG_WERT | int | Digital Wandler Wert von WaterValve Diag Wertbereich: 0..0x3FF (1023) PIN 44,PORT P5.15 |
| STAT_ZUSATZWASSERPUMPE_DIAG_EIN | int | Zusatzwasserpumpe Diag 0: Fehler, 1: In Ordnung Additional WaterPump Diag 0: ERR, 1: OK ShiftReg1Diagnostic.0 |
| STAT_FRONTWISCHER_DIAG_EIN | int | Frontwischer Ein/Aus Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet FrontWiper Switch Diag 0: LOW, 1: HIGH ShiftReg1Diagnostic.2 |
| STAT_FRONTWISCHER_GESCHW_DIAG_EIN | int | Frontwischer Geschwindigkeit Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet FrontWiper Speed Switch Diag 0: LOW, 1: HIGH ShiftReg1Diagnostic.3 |
| STAT_FH_FATH_AUF_DIAG_EIN | int | Fensterheber hinteren Fahrer Auf-Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet PowerWindow RearDriver OPEN Diag 0: LOW, 1: HIGH ShiftReg1Diagnostic.4 |
| STAT_FH_FATH_ZU_DIAG_EIN | int | Fensterheber hinteren Fahrer Zu-Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet PowerWindow RearDriver CLOSE Diag 0: LOW, 1: HIGH ShiftReg1Diagnostic.5 |
| STAT_FH_BFTH_AUF_DIAG_EIN | int | Fensterheber hinteren Beifahrer Auf-Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet PowerWindow RearPassenger OPEN Diag 0: LOW, 1: HIGH ShiftReg1Diagnostic.6 |
| STAT_FH_BFTH_ZU_DIAG_EIN | int | Fensterheber hinteren Beifahrer Zu-Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet PowerWindow RearPassenger CLOSE Diag 0: LOW, 1: HIGH ShiftReg1Diagnostic.7 |
| STAT_HECKWISCHER_DIAG_EIN | int | Heckwischer Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet RearWiper Diag 0: LOW, 1: HIGH ShiftReg2Diagnostic.0 |
| STAT_SRA_DIAG_EIN | int | Scheinwerferreinigung Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet HeadlampWasher Diag 0: LOW, 1: HIGH ShiftReg2Diagnostic.1 |
| STAT_ZV_VERRIEGELN_RELAIS_DIAG_EIN | int | Zentralverriegelung Verriegeln Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet CentralLocking LOCK Relay Diag 0: LOW, 1: HIGH ShiftReg2Diagnostic.2 |
| STAT_ZV_ENTRIEGELN_RELAIS_DIAG_EIN | int | Zentralverriegelung Entriegeln Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet CentralLocking UnLOCK Relay Diag 0: LOW, 1: HIGH ShiftReg2Diagnostic.3 |
| STAT_ZV_SICHERN_RELAIS_DIAG_EIN | int | Zentralverriegelung Sichern Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet CentralLocking SECURE Relay Diag 0: LOW, 1: HIGH ShiftReg2Diagnostic.4 |
| STAT_HECKSCHEIBENHEIZUNG_DIAG_EIN | int | Heckscheibenheizung Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet RearWindowHeater Diag 0: LOW, 1: HIGH ShiftReg2Diagnostic.5 |
| STAT_ZV_SELEKTIV_ENTRIEGELN_RELAY_DIAG_EIN | int | Zentralverriegelung selektives Entriegeln Relais Diag 0: Relais Abgeschaltet, 1: Relais Eingeschaltet CentralLocking LOCKDRIVER Relay Diag 0: LOW, 1: HIGH ShiftReg2Diagnostic.6 |
| STAT_SITZHEIZUNG_BF_DIAG_EIN | int | Sitzheizung Beifahrer Diag 0: Ausgang Nicht Aktiv, 1: Ausgang Aktiv SeatHeating Passenger Diag 0: LOW, 1: HIGH PIN 47,PORT P2.0 |
| STAT_SITZHEIZUNG_FA_DIAG_EIN | int | Sitzheizung Fahrer Diag 0: Ausgang Nicht Aktiv, 1: Ausgang Aktiv SeatHeating Driver Diag 0: LOW, 1: HIGH PIN 59,PORT P2.10 |
| STAT_HECKKLAPPE_DIAG_EIN | int | Heckklappe Diag 0: In Ordnung, 1: Fehler TrunkLid Diag 0: OK, 1: ERR_TRUNK_LID PIN 65,PORT P3.0 |
| STAT_HECKSCHEIBE_DIAG_EIN | int | Heckscheibe Diag 0: In Ordnung, 1: Fehler RearWindow Diag 0: OK, 1: ERR_REAR_WINDOW PIN 66,PORT P3.1 |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-internal-variables"></a>
### STATUS_INTERNAL_VARIABLES

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CAN_GESCHWINDIGKEIT_FAHRZEUG_WERT | unsigned int | Vehicle Speed (VS)[Km/h] PTCAN0x1A0_BYTE0_BYTE1 Zykluszeit: ttyp = 100ms (tmin = 95ms, tmax = 105ms) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich: 0..0xFFF (HEX)&lt;-&gt;0..350 [km/h] (PH) = 0,1 * (HEX)  [km/h] Sender: PT-CAN DSC_Modul |
| STAT_CAN_KILOMETERSTAND_WERT | unsigned long | Kilometre [Km] KCAN0x330_BYTE0_BYTE1_BYTE2 Zykluszeit: ttyp = 10s (tmin = 9s, tmax = 11s) Aktivbedingung = KL_R Startbedingung = KL_R_ON, Stopbedingung = KL_R_OFF Wertebereich:0..0xFFFFFF&lt;-&gt;0..16.777.214 [Km] Sender: K_CAN Kombi |
| STAT_CAN_RELATIVZEIT_WERT | unsigned long | Relative Time [s] KCAN0x328_BYTE0_BYTE1_BYTE2_BYTE3 Zykluszeit: ttyp = 1s (tmin = 0,9s, tmax = 1,1s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich:0..0xFFFFFFFF&lt;-&gt;0..4.294.967.294 [s] (136,9 jahres) Sender: K_CAN Kombi |
| STAT_CAN_REGENSENSOR_INTERVALL_ZEIT_WERT | unsigned int | Rain Sensor Interval Time KCAN0x226_BYTE1_BYTE2 Zykluszeit: ttyp = 8s (tmin = 7,2s, tmax = 8,8s) Aktivbedingung = KL_R Startbedingung = KL_R_ON, Stopbedingung = KL_R_OFF Wertebereich: 0..0xFFF (HEX)&lt;-&gt; 0: Sofort loswischen 1...0xFFFD(65533): Intervallzeit in 100 ms Schritten 65534: Nicht wischen (Pause),0xFFFF: Signal ungültig (PH) = 100 * (HEX)  [ms], 100 .. 6553300 ms Sender: K_CAN FZD |
| STAT_CAN_REGENSENSOR_WISCHER_GESCHW_WERT | int | Rain Sensor Wiper Speed KCAN0x226_BYTE3, BITS 0..3 Zykluszeit: ttyp = 8s (tmin = 7,2s, tmax = 8,8s) Aktivbedingung = KL_R Startbedingung = KL_R_ON, Stopbedingung = KL_R_OFF 0: Wischer ausschalten, 1...14: Stufe 1..14, 15: Signal ungültig (PH) = 2 * (HEX) + 33 [Wischhübe/min]: 35 .. 61 Wischhübe/min Sender: K_CAN FZD |
| STAT_CAN_REGENSENSOR_STATUS_WERT | int | Rain Sensor Status KCAN0x226_BYTE3, BITS 4..7 Zykluszeit: ttyp = 8s (tmin = 7,2s, tmax = 8,8s) Aktivbedingung = KL_R Startbedingung = KL_R_ON, Stopbedingung = KL_R_OFF ---0: Normaler Wischablauf ---1: Wasserschwall --0-: Wischer fährt bis Umkehrlage --1-: Wischer fährt bis Parkposition -0--: Regensensor in Ordnung -1--: Regensensor im Notlauf 1111: Signal ungültig Sender: K_CAN FZD |
| STAT_CAN_AUSSENTEMPERATUR_BUS_WERT | int | Value in Bus for Exterior Temperature (HEX) KCAN0x2CA_BYTE0 Zykluszeit: ttyp = 1s (tmin = 0,9s, tmax = 1,1s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich: 0&lt;-&gt;255 Sender: K_CAN Kombi |
| STAT_CAN_AUSSENTEMPERATUR_WERT | real | Exterior Temperature (T) [°C] Wertebereich:0..255 (HEX) (T)= 0,5 * (HEX)-40 [°C], -40..+85 [°C] |
| STAT_CAN_ZV_FA_WERT | int | CentralLocking Driver KCAN0x2A0_BYTE0, BITS 0-3 Zykluszeit: ttyp = 5s (tmin = 4s, tmax = 6s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF -0--: Kindersicherung deaktivieren -1--: Kindersicherung aktivieren 0-00: Elektrisch öffnen 0-01: Entriegeln 0-10: Verriegeln 0-11: Sichern 1000: Keine Anderung 1-01: Logisch entriegeln 1111: Signal ungültig Sender: K_CAN CAS |
| STAT_CAN_ZV_BF_WERT | int | CentralLocking Passenger KCAN0x2A0_BYTE0, BITS 4-7 Zykluszeit: ttyp = 5s (tmin = 4s, tmax = 6s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF -0--: Kindersicherung deaktivieren -1--: Kindersicherung aktivieren 0-00: Elektrisch öffnen 0-01: Entriegeln 0-10: Verriegeln 0-11: Sichern 1000: Keine Anderung 1-01: Logisch entriegeln 1111: Signal ungültig Sender: K_CAN CAS |
| STAT_CAN_ZV_FATH_WERT | int | CentralLocking RearDriver KCAN0x2A0_BYTE1, BITS 0-3 Zykluszeit: ttyp = 5s (tmin = 4s, tmax = 6s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF -0--: Kindersicherung deaktivieren -1--: Kindersicherung aktivieren 0-00: Elektrisch öffnen 0-01: Entriegeln 0-10: Verriegeln 0-11: Sichern 1000: Keine Anderung 1-01: Logisch entriegeln 1111: Signal ungültig Sender: K_CAN CAS |
| STAT_CAN_ZV_BFTH_WERT | int | CentralLocking RearPassenger KCAN0x2A0_BYTE1, BITS 4-7 Zykluszeit: ttyp = 5s (tmin = 4s, tmax = 6s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF -0--: Kindersicherung deaktivieren -1--: Kindersicherung aktivieren 0-00: Elektrisch öffnen 0-01: Entriegeln 0-10: Verriegeln 0-11: Sichern 1000: Keine Anderung 1-01: Logisch entriegeln 1111: Signal ungültig Sender: K_CAN CAS |
| STAT_CAN_ZV_HECKKLAPPE_WERT | int | CentralLocking TrunkLid KCAN0x2A0_BYTE2, BITS 0-3 Zykluszeit: ttyp = 5s (tmin = 4s, tmax = 6s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF -0--: Heckklappe -1--: Heckscheibe 0-00: Elektrisch öffnen 0-01: Entriegeln 0-10: Verriegeln 0-11: Sichern 1000: Keine Anderung 1-01: Logisch entriegeln 1111: Signal ungültig Sender: K_CAN CAS |
| STAT_CAN_ZV_TANKKLAPPE_WERT | int | CentralLocking FuelTank KCAN0x2A0_BYTE2, BITS 4-7 Zykluszeit: ttyp = 5s (tmin = 4s, tmax = 6s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF 0-00: Elektrisch öffnen 0-01: Entriegeln 0-10: Verriegeln 0-11: Sichern 1000: Keine Anderung 1-01: Logisch entriegeln 1111: Signal ungültig Sender: K_CAN CAS |
| STAT_CAN_TUERKONTAKT_FAT_EIN | int | DoorContact Driver KCAN0x24B_BYTE0, BITS 0-1 Zykluszeit: ttyp = 10s (tmin = 9s, tmax = 11s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF 0: FAT ist geschlossen 1: FAT ist offen 2: Signal unplausibel 3: Signal ungültig Sender: K_CAN FRMFA |
| STAT_CAN_TUERKONTAKT_FBT_EIN | int | DoorContact Passenger KCAN0x24B_BYTE0, BITS 2-3 Zykluszeit: ttyp = 10s (tmin = 9s, tmax = 11s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF 0: BFT ist geschlossen 1: BFT ist offen 2: Signal unplausibel 3: Signal ungültig Sender: K_CAN FRMFA |
| STAT_CAN_TUERKONTAKT_BFTH_EIN | int | DoorContact RearPassenger KCAN0x24B_BYTE0, BITS 4-5 Zykluszeit: ttyp = 10s (tmin = 9s, tmax = 11s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF 0: BFTH ist geschlossen 1: BFTH ist offen 2: Signal unplausibel 3: Signal ungültig Sender: K_CAN FRMFA |
| STAT_CAN_TUERKONTAKT_FATH_EIN | int | DoorContact RearDriver KCAN0x24B_BYTE0, BITS 6-7 Zykluszeit: ttyp = 10s (tmin = 9s, tmax = 11s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF 0: FATH ist geschlossen 1: FATH ist offen 2: Signal unplausibel 3: Signal ungültig Sender: K_CAN FRMFA |
| STAT_VAR_FH_FATH_BEFEHL_EIN | int | PowerWindow RearDriver Command 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_BFTH_BEFEHL_EIN | int | PowerWindow RearPassenger Command 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_BF_BEFEHL_EIN | int | PowerWindow Passenger Command 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_BFTH_POSITION_EIN | int | PowerWindow RearPassenger 0: UP, 1: MIDDLE, 2: DOWN, 3: UNK |
| STAT_VAR_FH_FATH_POSITION_EIN | int | PowerWindow RearDriver 0: UP, 1: MIDDLE, 2: DOWN, 3: UNK |
| STAT_VAR_FH_FATH_SCHALTER_EIN | int | PowerWindow RearDriver Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_BFTH_SCHALTER_EIN | int | PowerWindow RearPassenger Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_FATH_FA_SCHALTER_EIN | int | PowerWindowDriver RearDriver Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_BFTH_FA_SCHALTER_EIN | int | PowerWindowDriver RearPassenger Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_ZV_LETZTER_BEFEHL_EIN | int | CentralLocking LastCommand 0: OFF, 1: ER, 2: VR, 3: VRZS, 4: SER, 5: ES |
| STAT_VAR_ZV_BEFEHL_EIN | int | CentralLocking Command 0: OFF, 1: ER, 2: VR, 3: VRZS, 4: SER, 5: ES |
| STAT_VAR_HECKKLAPPE_BEFEHL_EIN | int | TrunkLid CAN Command 0: OFF, 1: ON |
| STAT_VAR_HECKSCHEIBE_BEFEHL_EIN | int | RearWindow CAN Command 0: OFF, 1: ON |
| STAT_VAR_LETZTER_HECKKLAPPE_KONTAKT_EIN | int | Last TrunkLid Contact 0: OFF, 1: ON |
| STAT_VAR_LETZTER_HECKSCHEIBE_KONTAKT_EIN | int | Last RearWindow Contact 0: OFF, 1: ON |
| STAT_VAR_HECKKLAPPE_WIEDERHOLSPERRE_EIN | int | TrunkLid Repetition Block 0: OFF, 1: ON |
| STAT_VAR_ZV_WIEDERHOLSPERRE_EIN | int | CentralLocking Repetition Block 0: OFF, 1: ON |
| STAT_VAR_FH_FREISCHALTUNG_EIN | int | PowerWindow Enable 0: DISABLE, 1: ENABLE Wert am VAR umgekehrt! Actual Value Inverted! |
| STAT_VAR_HECKSCHEIBE_WIEDERHOLSPERRE_EIN | int | RearWindow Repetition Block 0: OFF, 1: ON |
| STAT_VAR_RUECKWAERTSGANG_EIN | int | Reverse Gear 0: OFF, 1: ON |
| STAT_VAR_FRONTWISCHER_WIEDERHOLSPERRE_FLAG_EIN | int | FrontWiper Blocking Flag 0: OFF, 1: ON |
| STAT_VAR_WASSERVENTIL_BEFEHL_EIN | int | WaterValve Command 0: CLOSE, 1: OPEN, 2: OPEN30 |
| STAT_VAR_HECKWISCHER_WIEDERHOLSPERRE_FLAG_EIN | int | RearWiper Blocking Flag 0: OFF, 1: ON |
| STAT_VAR_WASCHERPUMPE_TIMEOUTRESET_EIN | int | WaterPump TimeoutReset 0: OFF, 1: ON |
| STAT_VAR_FH_FATH_TEMPERATURSCHUTZ_FLAG_EIN | int | PowerWindow RearDriver ThermalProtection Flag 0: OFF, 1: ON |
| STAT_VAR_FH_BFTH_TEMPERATURSCHUTZ_FLAG_EIN | int | PowerWindow RearPassenger ThermalProtection Flag 0: OFF, 1: ON |
| STAT_VAR_FH_THERMALSLEEP_EIN | int | PowerWindow ThermalSleep 0: Normal, 1: 1minSleeping, 2: GoneToSleep 3: RelTimeAfterWakeUp, 4: OutsideTempAfterWakeUp 5: Time&TempAfterWakeUp |
| STAT_VAR_ERROROUTTEMP_EIN | int | Sec. without receiving msg. "Outside Temperature" 0..7 [sec] |
| STAT_VAR_FRONTWISCHER_BEFEHL_EIN | int | FrontWiper Command 0: OFF, 1: STATE1, 2: STATE2, 3: INTERVAL, 4: TIPPWISHEN |
| STAT_VAR_FRONTWISCHER_POTI_EIN | int | FrontWiper Potentiometer 0: POS0, 1: POS1, 2: POS2, 3: POS3 |
| STAT_VAR_HECKWISCHER_BEFEHL_EIN | int | RearWiper Command 0: OFF, 1: ON |
| STAT_VAR_WASCHERPUMPE_BEFEHL_EIN | int | WasherPump Command 0: OFF, 1: FRONT, 2: REAR |
| STAT_VAR_HECKWASCHERPUMPE_FLAG_EIN | int | WasherPump RearWiper Flag 0: OFF, 1: ON |
| STAT_VAR_SRA_PUMPE_FLAG_EIN | int | WasherPump HeadlampWasher Flag 0: OFF, 1: ON |
| STAT_VAR_SITZHEIZUNG_FA_BEFEHL_EIN | int | SeatHeating Driver Command 0: OFF, 1: STATE1, 2: STATE2, 3: STATE3 |
| STAT_VAR_SITZHEIZUNG_BF_BEFEHL_EIN | int | SeatHeating Passenger Command 0: OFF, 1: STATE1, 2: STATE2, 3: STATE3 |
| STAT_VAR_CRASH_FLAG_EIN | int | Crash Flag 0: OFF, 1: ON |
| STAT_VAR_FRONTWASCHERPUMPE_FLAG_EIN | int | WasherPump FrontWiper Flag 0: OFF, 1: ON |
| STAT_VAR_HECKSCHEIBENHEIZUNG_BEFEHL_EIN | int | RearWindow Heater Command 0: OFF, 1: ON |
| STAT_VAR_WASSERPUMPE_BEFEHL_EIN | int | WaterPump Command 0: OFF, 1: ON |
| STAT_VAR_SONNENROLLO_BEFEHL_EIN | int | Sunblind Command KCAN0x26D_BYTE0, BITS 0..1 Entprellzeit: tmin = 100 ms Aktivbedingung = BUS_AKTIV Sendebedingung = SIGNALCHANGE 0: OFF, 1: ON Sender: K-CAN IHK |
| STAT_VAR_SITZHEIZUNG_FA_SCHALTER_EIN | int | SeatHeating Driver Button 0: OFF, 1: ON |
| STAT_VAR_SITZHEIZUNG_BF_SCHALTER_EIN | int | SeatHeating Passenger Button 0: OFF, 1: ON |
| STAT_VAR_KLEMMEN58G_EIN | int | Klemmen58g 0: OFF, 1: ON |
| STAT_VAR_AUCSENSOR_FLAG_EIN | int | AUCSensor Flag 0: OFF, 1: ON |
| STAT_VAR_REGENSENSOR_BOTSCHAFT_FEHLER_EIN | int | Non RegenSensor Message 0: OFF, 1: ON |
| STAT_VAR_KOMPRESSOR_BEFEHL_EIN | int | Compressor DutyCycle (Kompression in %) KCAN0x246_BYTE2 Zykluszeit: ttyp = 1s (tmin = 0,9s, tmax = 1,1s) Aktivbedingung = KL_15 Startbedingung = KL_15_ON, Stopbedingung = KL_15_OFF Wertebereich: 0..100&lt;-&gt;0..100 [%], 255 Signal ungültig Sender: K-CAN JBBFE |
| STAT_VAR_KLEMMEN_R_EIN | int | Klemmen R 0: OFF, 1: ON |
| STAT_VAR_KLEMMEN_15_EIN | int | Klemmen 15 0: OFF, 1: ON |
| STAT_VAR_KLEMMEN_50_EIN | int | Klemmen 50 0: OFF, 1: ON |
| STAT_VAR_KLEMMEN_61_EIN | int | Klemmen 61 0: OFF, 1: START, 2: GO |
| STAT_VAR_DRUCKSENSOR_WERT_EIN | int | Pressure Sensor KCAN0x2D2_BYTE0 Zykluszeit: ttyp = 20s (tmin = 18s, tmax = 22s) Aktivbedingung = KL_15 Startbedingung = KL_15_ON, Stopbedingung = KL_15_OFF Wertebereich: 0..0x46(70) [HEX], 255 Signal ungültig (PH) = 0,5 * (HEX) [bar],0..35 [bar] Sender: K-CAN JBBFE |
| STAT_VAR_FONDSCHICHTUNGSSENSOR_WERT | int | Rear Airflow KCAN0x2D3_BYTE0 Zykluszeit: ttyp = 20s (tmin = 18s, tmax = 22s) Aktivbedingung = KL_15 Startbedingung = KL_15_ON, Stopbedingung = KL_15_OFF Wertebereich: 0..100 [%], 255 Signal ungültig Sender: K-CAN JBBFE |
| STAT_VAR_KOMPRESSORVENTIL_MAX_STROM_WERT | int | Compressor MaxCurrent |
| STAT_VAR_TANK_FA_WIDERSTAND_WERT | int | ACHTUNG: Tankgeber links!!! Auch bei RL FuelTankLeft Resistance KCAN0x349_BYTE0_BYTE1 Zykluszeit: ttyp = 200ms (tmin = 180ms, tmax = 220ms) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich: 0..2F26 [HEX], 0xFFFF Signal ungültig (PH) = 0,1 * (HEX) [Ohm], 0..1207 [Ohm] Sender: K-CAN JBBFE |
| STAT_VAR_TANK_BF_WIDERSTAND_WERT | int | ACHTUNG: Tankgeber rechts!!! Auch bei RL FuelTankRechts Resistance KCAN0x349_BYTE0_BYTE1 Zykluszeit: ttyp = 200ms (tmin = 180ms, tmax = 220ms) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich: 0..2F26 [HEX], 0xFFFF Signal ungültig (PH) = 0,1 * (HEX) [Ohm], 0..1207 [Ohm] Sender: K-CAN JBBFE |
| STAT_VAR_AUCSENSOR_BEFEHL_EIN | int | AUC Sensor Command 0: LGSI, 1: LGS0, 2: LGS1, 3: LGS2, 4: LGS3 5: LGS4, 6: LGS5, 7: LGS6, 8: LGSE |
| STAT_VAR_AUCSENSOR_LEZTER_BEFEHL_EIN | int | AUCSensor LastCommand 0: LGSI, 1: LGS0, 2: LGS1, 3: LGS2, 4: LGS3 5: LGS4, 6: LGS5, 7: LGS6, 8: LGSE |
| STAT_VAR_BATTERIE_SPANNUNG_KLASSE_EIN | int | Battery Voltage Class 0: CLASS0, 1: CLASS1, 2: CLASS2, 3: CLASS3, 4: CLASS4 5: CLASS5, 6: CLASS6, 7: CLASS7 |
| STAT_VAR_FAHRZEUG_GESCHW_KLASSE_EIN | int | Vehicle Speed Class 0: CLASS0, 1: CLASS1, 2: CLASS2, 3: CLASS3, 4: CLASS4, 5: CLASS5 |
| STAT_VAR_KUEHLMITTELSTAND_SCHWELLE_FLAG_EIN | int | Coolant Threshold Flag 0: OFF, 1: ON |
| STAT_VAR_WASCHWASSERSTAND_SCHWELLE_FLAG_EIN | int | WaterThreshold Flag 0: OFF, 1: ON |
| STAT_VAR_DISABLEMSGTX_EIN | int | Disable Msg. Tx 0: ENABLE, 1: DISABLE |
| STAT_VAR_FH_FATH_KOMFORT_BEFEHL_EIN | int | PowerWindow RearDriver Comfort Command 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_BFTH_KOMFORT_BEFEHL_EIN | int | PowerWindow RearPassenger Comfort Command 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO |
| STAT_VAR_FH_KINDERSICHERUNG_EIN | int | PowerWindow Child Safety 0: OFF, 1: ON |
| STAT_VAR_KOMPRESSORVENTIL_AUSGANG_EIN | int | Compressor Ventil Output 0: OFF, 1: ON, 3: INVALID |
| STAT_VAR_CRANK_STATUS_EIN | int | Crank State 0: OFF, 1: ON |
| STAT_VAR_WASCHDUESENTEST_STATUS_EIN | int | JetWasher Test Status 0: NOT_ACTIVE, 1: ACTIVE |
| STAT_VAR_FH_FREISCHALTUNG_PANIK_EIN | int | Enable Power Window Panic Mode 0: DISABLE, 1: ENABLE |
| STAT_VAR_FH_FAT_CAN_VERLOREN_EIN | int | PowerWindow Driver Message Lost 0: Message NOT LOST, 1: Message LOST |
| STAT_VAR_PWRD_TEMP_WERT | real | PowerWindow Driver motor internal temperature -40000...+119000 --&gt; -40°C...+119°C |
| STAT_VAR_PWRP_TEMP_WERT | real | PowerWindow Passenger motor internal temperature -40000...+119000 --&gt; -40°C...+119°C |
| STAT_VAR_RD_H1_ERR_EIN | int | Power Window Rear Driver Hall Sensor1 Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_RD_H2_ERR_EIN | int | Power Window Rear Driver Hall Sensor2 Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_RD_RU_ERR_EIN | int | Power Window Rear Driver Relay Up Stuck Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_RD_RD_ERR_EIN | int | Power Window Rear Driver Relay Down Stuck Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_RP_H1_ERR_EIN | int | Power Window Rear Passenger Hall Sensor1 Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_RP_H2_ERR_EIN | int | Power Window Rear Passenger Hall Sensor2 Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_RP_RU_ERR_EIN | int | Power Window Rear Passenger Relay Up Stuck Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_RP_RD_ERR_EIN | int | Power Window Rear Passenger Relay Down Stuck Error 0: There is Not DTC: 0, 1: There is DTC |
| STAT_VAR_FH_FATH_UNNORM_EIN | int | Cause for the last PowerWindow RearDriver denorming 0..0x0F |
| STAT_VAR_FH_BFTH_UNNORM_EIN | int | Cause for the last PowerWindow RearPassenger denorming 0..0x0F |
| STAT_VAR_SITZHEIZUNG_FA_FREISCHALTUNG_EIN | int | SeatHeating Driver Enabled 0: OFF, 1: ON |
| STAT_VAR_SITZHEIZUNG_BF_FREISCHALTUNG_EIN | int | SeatHeating Passenger Enabled 0: OFF, 1: ON |
| STAT_VAR_SITZHEIZUNG_ANSWER_EIN | int | SeatHeating Answer 0: OFF, 1: ON |
| STAT_VAR_RUECKWAERTSGANG_BA_EIN | int | ReverseGearBA 0: OFF, 1: ON |
| STAT_VAR_RUECKWAERTSGANG_3B0_EIN | int | ReverseGear3B0 0: OFF, 1: ON |
| STAT_VAR_FH_FATH_AP_START_INIT_EIN | int | PowerWindow RearDriver AP_Start_Init 0: OFF, 1: ON |
| STAT_VAR_FH_BFTH_AP_START_INIT_EIN | int | PowerWindow RearPassenger AP_Start_Init 0: OFF, 1: ON |
| STAT_VAR_CLSTATUS_FAT_EIN | int | Status CentralLocking Driver Door 0: cl_OFF, 1: cl_ER, 2: cl_VR, 3: cl_VRZS, 4: cl_SER, 5: cl_ES |
| STAT_VAR_CLSTATUS_BFT_EIN | int | Status CentralLocking Passenger Door 0: cl_OFF, 1: cl_ER, 2: cl_VR, 3: cl_VRZS, 4: cl_SER, 5: cl_ES |
| STAT_VAR_CLSTATUS_FATH_EIN | int | Status CentralLocking RearDriver Door 0: cl_OFF, 1: cl_ER, 2: cl_VR, 3: cl_VRZS, 4: cl_SER, 5: cl_ES |
| STAT_VAR_CLSTATUS_BFTH_EIN | int | Status CentralLocking RearPassenger Door 0: cl_OFF, 1: cl_ER, 2: cl_VR, 3: cl_VRZS, 4: cl_SER, 5: cl_ES |
| STAT_VAR_CLSTATUS_HK_EIN | int | Status CentralLocking TrunkLid 0: cl_OFF, 1: cl_ER, 2: cl_VR, 3: cl_VRZS, 4: cl_SER, 5: cl_ES |
| STAT_CAN_BEDIENUNG_ZVFAT_EIN | int | DoorContact RearDriver KCAN0x24B_BYTE1, BITS 0-3 Zykluszeit: ttyp = 10s (tmin = 9s, tmax = 11s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF 0: FATH ist geschlossen 1: FATH ist offen 2: Signal unplausibel 3: Signal ungültig Sender: K_CAN FRMFA |
| STAT_VAR_TUERKONTAKT_FAT_LETZT_EIN | int | DoorContact Driver Last 0: FAT ist geschlossen 1: FAT ist offen 2: Signal unplausibel 3: Signal ungültig |
| STAT_VAR_TUERKONTAKT_FBT_LETZT_EIN | int | DoorContact Passenger Last 0: BFT ist geschlossen 1: BFT ist offen 2: Signal unplausibel 3: Signal ungültig |
| STAT_VAR_TUERKONTAKT_BFTH_LETZT_EIN | int | DoorContact RearPassenger Last 0: BFTH ist geschlossen 1: BFTH ist offen 2: Signal unplausibel 3: Signal ungültig |
| STAT_VAR_TUERKONTAKT_FATH_LETZT_EIN | int | DoorContact RearDriver Last 0: FATH ist geschlossen 1: FATH ist offen 2: Signal unplausibel 3: Signal ungültig |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-input"></a>
### STEUERN_DIGITAL_INPUT

Digitale Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table DigitalInputNrTexte DINNR TEXT |
| WERT | string | table DigitalInputNrTexte WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DIGITAL_INPUT_STATUS | string | DIGITAL_INPUT_SET or ERROR_IN_ADDR or ERROR_IN_VALUE |
| DIGITAL_INPUT_ADDR | string | ort |
| DIGITAL_INPUT_VALUE | string | wert |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-output"></a>
### STEUERN_DIGITAL_OUTPUT

Digitale Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Ouput $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table DigitalOutputNrTexte DOUTNR NAME |
| WERT | string | table DigitalOutputNrTexte WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DIGITAL_OUTPUT_STATUS | string | DIGITAL_OUTPUT_SET or ERROR_IN_ADDR or ERROR_IN_VALUE |
| DIGITAL_OUTPUT_ADDR | string | ort |
| DIGITAL_OUTPUT_VALUE | string | wert |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-analog-input"></a>
### STEUERN_ANALOG_INPUT

Analoge Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Input $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table AnalogInputNrTexte AINNR NAME |
| WERT | string | table AnalogInputNrTexte WERT |
| ART_WERT | string | "nein"-&gt; ADC register Wert "ja"  -&gt; (PH) Wert table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANALOG_INPUT_STATUS | string | ANALOG_INPUT_SET or ERROR_IN_ADDR or ERROR_IN_VALUE |
| ANALOG_INPUT_ADDR | string | ort |
| ANALOG_INPUT_VALUE | string | wert |
| ANALOG_INPUT_CONVERTED_VALUE | string | wert from JBBE (ADC oder (PH)) |
| ANALOG_INPUT_ART_WERT | string | art wert: ADC oder (PH) |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-analog-output"></a>
### STEUERN_ANALOG_OUTPUT

Analoge Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Output $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table AnalogOutputNrTexte AOUTNR NAME |
| WERT | string | table AnalogOutputNrTexte WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANALOG_OUTPUT_STATUS | string | ANALOG_OUTPUT_SET or ERROR_IN_ADDR or ERROR_IN_VALUE |
| ANALOG_OUTPUT_ADDR | string | ort |
| ANALOG_OUTPUT_VALUE | string | wert |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult SATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sense-input"></a>
### STEUERN_SENSE_INPUT

Diagnostic Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $05 Digitale Input $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table SenseInputNrTexte SINNR NAME |
| WERT | string | table SenseInputNrTexte WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SENSE_INPUT_STATUS | string | SENSEL_INPUT_SET or ERROR_IN_ADDR or ERROR_IN_VALUE |
| SENSE_INPUT_ADDR | string | ort |
| SENSE_INPUT_VALUE | string | wert |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-beenden"></a>
### STEUERN_BEENDEN

Kontrolle an JBBFE zurueckgeben KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $02 Digitale Output $03 Analoge Input $04 Analoge Output $05 Sense Input $00 ReturnControToECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag1 an SG Digitale Input |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag2 an SG Digitale Output |
| _TEL_AUFTRAG3 | binary | Hex-Auftrag3 an SG Analoge Input |
| _TEL_AUFTRAG4 | binary | Hex-Auftrag4 an SG Analoge Output |
| _TEL_AUFTRAG5 | binary | Hex-Auftrag5 an SG Sense Input |
| _TEL_ANTWORT1 | binary | Hex-Antwort1 von SG Digitale Input |
| _TEL_ANTWORT2 | binary | Hex-Antwort2 von SG Digitale Output |
| _TEL_ANTWORT3 | binary | Hex-Antwort3 von SG Analoge Input |
| _TEL_ANTWORT4 | binary | Hex-Antwort4 von SG Analoge Output |
| _TEL_ANTWORT5 | binary | Hex-Antwort5 von SG Sense Input |

<a id="job-fs-lesen-lear"></a>
### _FS_LESEN_LEAR

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |
| F_TYPE | char | gewaehlter Option |

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

<a id="job-kompressor-parameters-write"></a>
### KOMPRESSOR_PARAMETERS_WRITE

Schreiben die kompressor parameters KWP2000: $3B WriteDataByLocalIdentifier $7C RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KOMP_GROSS_ANF_MIN | char |  |
| KOMP_GROSS_ANF_MAX | char |  |
| KOMP_GROSS_STR_MIN | char |  |
| KOMP_GROSS_STR_MAX | char |  |
| KOMP_KLEIN_ANF_MIN | char |  |
| KOMP_KLEIN_ANF_MAX | char |  |
| KOMP_KLEIN_STR_MIN | char |  |
| KOMP_KLEIN_STR_MAX | char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-kompressor-parameters-read"></a>
### KOMPRESSOR_PARAMETERS_READ

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $21 ReadDataByLocalIdentifier $7C RecordLocalId

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fueltank-parameters-reset"></a>
### FUELTANK_PARAMETERS_RESET

Schreiben die fullstand parameters KWP2000: $3B WriteDataByLocalIdentifier $7B RecordLocalId

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fueltank-parameters-read"></a>
### FUELTANK_PARAMETERS_READ

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $21 ReadDataByLocalIdentifier $7B RecordLocalId

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-l4969-registers"></a>
### READ_L4969_REGISTERS

Schreiben die fullstand parameters KWP2000: $21 ReadDataByLocalIdentifier $7A RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | ON or OFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| REG_VALUE | int | register value |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-historienspeicher-lesen-block-1"></a>
### STATUS_HISTORIENSPEICHER_LESEN_BLOCK_1

EnergieDatenSpeicher Teil 1 -Einschlafverhinderer- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE1 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DATENSATZ_1 | string | Datensatztext |
| STAT_VERURSACHER_1 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_1 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_1 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_1 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_2 | string | Datensatztext |
| STAT_VERURSACHER_2 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_2 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_2 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_2 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_3 | string | Datensatztext |
| STAT_VERURSACHER_3 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_3 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_3 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_3 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_4 | string | Datensatztext |
| STAT_VERURSACHER_4 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_4 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_4 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_4 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_5 | string | Datensatztext |
| STAT_VERURSACHER_5 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_5 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_5 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_5 | string | Einheit fuer KM_STAND: KM |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-historienspeicher-lesen-block-2"></a>
### STATUS_HISTORIENSPEICHER_LESEN_BLOCK_2

EnergieDatenSpeicher Teil 2 -Wecker- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DATENSATZ_0 | string | Datensatztext |
| STAT_RELATIVZEIT_BEGINN_WERT_0 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_0 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_0 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_0 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_0 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_0 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_0 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_0 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_0 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_1 | string | Datensatztext |
| STAT_RELATIVZEIT_BEGINN_WERT_1 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_1 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_1 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_1 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_1 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_1 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_1 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_1 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_2 | string | Datensatztext |
| STAT_RELATIVZEIT_BEGINN_WERT_2 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_2 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_2 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_2 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_2 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_2 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_2 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_2 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_3 | string | Datensatztext |
| STAT_RELATIVZEIT_BEGINN_WERT_3 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_3 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_3 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_3 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_3 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_3 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_3 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_3 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_4 | string | Datensatztext |
| STAT_RELATIVZEIT_BEGINN_WERT_4 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_4 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_4 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_4 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_4 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_4 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_4 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_4 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_5 | string | Datensatztext |
| STAT_RELATIVZEIT_BEGINN_WERT_5 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_5 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_5 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_5 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_5 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_5 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_5 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_5 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-historienspeicher-loeschen"></a>
### STEUERN_HISTORIENSPEICHER_LOESCHEN

EnergieDatenSpeicher Teil 1 und TEIL 2 loeschen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE0 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-version-gatewaymodules"></a>
### STATUS_VERSION_GATEWAYMODULES

Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6F RecordLocalId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERSION_GATEWAYTABELLE | long | Versionsnummer der Gateway-Tabelle |
| STAT_VERSION_GATEWAYSOFTWARE | long | Versionsnummer der Gateway-Software |
| STAT_VERSION_APPLSOFTWARE | string | Versionsnummer der Application Software |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode-funktional"></a>
### SLEEP_MODE_FUNKTIONAL

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |
| OHNE_POWERMODUL | string | Power Down ohne Powermodul Werte: JA, NEIN table DigitalArgument TEXT Defaultwert: NEIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-einlernen"></a>
### STEUERN_FENSTERHEBER_EINLERNEN

Init apinch through diagnosis KWP2000: $22   ReadDataByCommonIdentifier $0001 project specific. Init apinch

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | 0, 1 oder 2. FAH, BFH oder beide table InitApinch AUSWAHL_FH MODE_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fensterheber"></a>
### STATUS_FENSTERHEBER

Init apinch through diagnosis KWP2000: $22   ReadDataByCommonIdentifier $0004 project specific. Status apinch

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FAH_FH_FAEHRT_EIN | int | Driver door  is learning YES, when learning table LearningResult STATUS_TEXT |
| STAT_BFH_FH_FAEHRT_EIN | int | Passenger door is learning YES, when learning table LearningResult STATUS_TEXT |
| STAT_FAH_FH_EINGELERNT_EIN | int | Driver door  has learned YES, if learned table LearningResult STATUS_TEXT |
| STAT_BFH_FH_EINGELERNT_EIN | int | Passenger door has learned YES, if learned table LearningResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-denormieren"></a>
### STEUERN_FENSTERHEBER_DENORMIEREN

Init apinch through diagnosis KWP2000: $22   ReadDataByCommonIdentifier $0005 project specific. Init apinch

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | 0, 1 oder 2. FAH, BFH oder beide table UnnormApinch AUSWAHL_FH MODE_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-hinten"></a>
### STEUERN_FENSTERHEBER_HINTEN

Rear windows direkte ansteuern Ohne EKS, direkte Ausgang Steuerung Mit EKS, Steuerung ändernde Eingang und durch Application KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Ouput $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | 0: BFH, 1: FAH, 2: Beide Beide  Default table SteuernRearWindows AUSWAHL_FH |
| WERT | string | 0: Aus, 1: Auf, 2: Zu Aus Default table SteuernRearWindows WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_FENSTERHEBER_HINTEN_STATUS | string | STEUERN_FENSTERHEBER_HINTEN_SET or ERROR_IN_AUSWAHL_FH or ERROR_IN_WERT |
| STEUERN_FENSTERHEBER_HINTEN_AUSWAHL_FH | string | ort |
| STEUERN_FENSTERHEBER_HINTEN_WERT | string | wert |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-variant"></a>
### READ_VARIANT

Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6E RecordLocalId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VARIANT | string | Variant 0 = LOW 1 1 = LOW 2 2 = HIGH 1 3 = HIGH 2 4 = HIGH 3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-jbbfe-configuration"></a>
### _JBBFE_CONFIGURATION

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $7A RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VARIANT_BYTE | string | Variant 0 = Low 1 1 = Low 2 2 = High 1 3 = High 2 4 = High 3 5 = High 4 |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TTMMJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| SERIENUMMER | string | serial number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-log"></a>
### STATUS_FH_LOG

Ursachen der letzten Unnormalisierung des Fensters KWP2000: $22   ReadDataByCommonIdentifier $0008 project specific. Status Fensters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FENSTERHEBER_FAHRER_HINTEN_WERT | int | Fensterheber fahrer hinten stat wert |
| STAT_FENSTERHEBER_FAHRER_HINTEN_TEXT | string | 0x00: Nie denormalisiert 0x01: Fehler Hall Sensor 1 0x02: Fehler Hall Sensor 2 0x03: Fehler Hall Sensor 1 und 2 0x04: Fehler Relais zu 0x05: Fehler Hall Sensor 1 und Fehler Relais zu 0x06: Fehler Hall Sensor 2 und Fehler Relais zu 0x07: Fehler Hall Sensor 1 und 2 und Fehler Relais zu 0x08: Fehler Relais auf 0x09: Fehler Hall Sensor 1 und Fehler Relais auf 0x0A: Fehler Hall Sensor 2 und Fehler Relais auf 0x0B: Fehler Hall Sensor 1 und 2 und Fehler Relais auf 0x0C: Fehler Relais zu und auf 0x0D: Fehler Hall Sensor 1 und Fehler Relais zu und auf 0x0E: Fehler Hall Sensor 2 und Fehler Relais zu und auf 0x0F: Fehler Hall Sensor 1 und 2 und Fehler Relais zu und auf 0x10: Fehler Einklemmschutz Daten Gruppe 0x20: Kein Einklemmschutz war codiert 0x30: Der Schalter war in Richtung Maut Öffnen zwischen 15 und 20 Sekunden betätigt 0x40: Steuern_Fensterheber_Denormieren 0x50: Steuern_Fensterheber_Einlernen unterbrochen durch Schalter betätigt 0x60: Steuern_Fensterheber_Einlernen unterbrochen durch einen Komfort Nachrichten 0x70: Steuern_Fensterheber_Einlernen unterbrochen durch Thermoschutz 0x80: Steuern_Fensterheber_Einlernen unterbrechet durch Überstrom (I&gt;27A) 0x90: Steuern_Fensterheber_Einlernen unterbrochen durch Wiederholsperre 0xA0: Steuern_Fensterheber_Einlernen unterbrochen durch eine Reversierung 0xB0: Steuern_Fensterheber_Einlernen unterbrochen durch ein Fehler in die Batteriespannung, Unterspannung (Ub&lt;9V) oder Überspannung (Ub&gt;16V) 0xFF: Achtung!!!. EEPROM nicht initialisiert |
| STAT_FENSTERHEBER_BEIFAHRER_HINTEN_WERT | int | Fensterheber beifahrer hinten stat wert |
| STAT_FENSTERHEBER_BEIFAHRER_HINTEN_TEXT | string | 0x00: Nie denormalisiert 0x10: Fehler Hall Sensor 1 0x20: Fehler Hall Sensor 2 0x30: Fehler Hall Sensor 1 und 2 0x40: Fehler Relais zu 0x50: Fehler Hall Sensor 1 und Fehler Relais zu 0x60: Fehler Hall Sensor 2 und Fehler Relais zu 0x70: Fehler Hall Sensor 1 und 2 und Fehler Relais zu 0x80: Fehler Relais auf 0x90: Fehler Hall Sensor 1 und Fehler Relais auf 0xA0: Fehler Hall Sensor 2 und Fehler Relais auf 0xB0: Fehler Hall Sensor 1 und 2 und Fehler Relais auf 0xC0: Fehler Relais zu und auf 0xD0: Fehler Hall Sensor 1 und Fehler Relais zu und auf 0xE0: Fehler Hall Sensor 2 und Fehler Relais zu und auf 0xF0: Fehler Hall Sensor 1 und 2 und Fehler Relais zu und auf 0x01: Fehler Einklemmschutz Daten Gruppe 0x02: Kein Einklemmschutz war codiert 0x03: Der Schalter war in Richtung Maut Öffnen zwischen 15 und 20 Sekunden betätigt 0x04: Steuern_Fensterheber_Denormieren 0x05: Steuern_Fensterheber_Einlernen unterbrochen durch Schalter betätigt 0x06: Steuern_Fensterheber_Einlernen unterbrochen durch einen Komfort Nachrichten 0x07: Steuern_Fensterheber_Einlernen unterbrochen durch Thermoschutz 0x08: Steuern_Fensterheber_Einlernen unterbrechet durch Überstrom (I&gt;27A) 0x09: Steuern_Fensterheber_Einlernen unterbrochen durch Wiederholsperre 0x0A: Steuern_Fensterheber_Einlernen unterbrochen durch eine Reversierung 0x0B: Steuern_Fensterheber_Einlernen unterbrochen durch ein Fehler in die Batteriespannung, Unterspannung (Ub&lt;9V) oder Überspannung (Ub&gt;16V) 0xFF: Achtung!!!. EEPROM nicht initialisiert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-check-dtc-memo"></a>
### _CHECK_DTC_MEMO

Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6D RecordLocalId Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POSITION | char | Variant Position in EE_Failures array Byte 0 Code Byte 1 Counter Byte 2 Symptom, Readiness, Memory, Active and Warning Byte 3 Logistic Counter Bytes 4 & 5 Milage Bytes 6 & 7 Geschwindigkeit Byte 8 & 9 Batteryspannung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen-selektiv"></a>
### FS_LOESCHEN_SELEKTIV

Fehlerspeicher loeschen Selektiv KWP2000: $14 ClearDiagnosticInformation Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | string | Fehlerspeicher zu loeschen z.b. 0xAAAA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lear-sleep-mode"></a>
### _LEAR_SLEEP_MODE

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $FA LearPowerDown Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-waschduese-aussenspiegel"></a>
### STEUERN_WASCHDUESE_AUSSENSPIEGEL

Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $79 RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTRO_JWH_TIMER | unsigned int | Control the Jet Washer and Mirror Heater for the time: CONTRO_JWH_TIMER * 10ms. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-position"></a>
### STATUS_FH_POSITION

Lesen der FH position KWP2000: $21 ReadDataByLocalIdentifier $79 RecordLocalId

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_FENSTERHEBER_FAHRER_HINTEN_WERT | long | Rear Driver PW Pulses |
| STAT_FENSTERHEBER_FAHRER_HINTEN_CM | long | Rear Driver PW Position in cm |
| STAT_FENSTERHEBER_BEIFAHRER_HINTEN_WERT | long | Rear Passenger PW Pulses |
| STAT_FENSTERHEBER_BEIFAHRER_HINTEN_CM | long | Rear Passenger PW Position in cm |

<a id="job-steuern-wasserventil"></a>
### STEUERN_WASSERVENTIL

Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $78 RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_WV_TIMER | unsigned int | Control the WasserVentil for the time: CONTROL_WV_TIMER * 10ms. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zwp"></a>
### STEUERN_ZWP

Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $77 RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_ZWP_TIMER | unsigned int | Control the Additional Water Pump (ZWP) for the time: CONTROL_ZWP_TIMER * 10ms. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (10 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (57 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (6 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (2 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (5 × 9)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [DIGITALINPUTNRTEXTE](#table-digitalinputnrtexte) (11 × 4)
- [DIGITALOUTPUTNRTEXTE](#table-digitaloutputnrtexte) (52 × 4)
- [ANALOGINPUTNRTEXTE](#table-analoginputnrtexte) (13 × 4)
- [ANALOGOUTPUTNRTEXTE](#table-analogoutputnrtexte) (6 × 4)
- [SENSEINPUTNRTEXTE](#table-senseinputnrtexte) (23 × 4)
- [FUNKTIONALEADRESSE](#table-funktionaleadresse) (8 × 3)
- [INITAPINCH](#table-initapinch) (7 × 3)
- [LEARNINGRESULT](#table-learningresult) (3 × 2)
- [UNNORMAPINCH](#table-unnormapinch) (7 × 3)
- [STEUERNREARWINDOWS](#table-steuernrearwindows) (10 × 4)
- [VARIANT_TABLE](#table-variant-table) (7 × 3)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 4 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
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

Dimensions: 76 rows × 2 columns

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
| 0x72 | ASIN AWCO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
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
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Anlieferzustand |
| 0x01 | Normalbetrieb |
| 0x02 | nicht benutzt |
| 0x03 | Speicher gelöscht |
| 0x04 | nicht benutzt |
| 0x05 | Signaturprüfung PAF nicht durchgeführt |
| 0x06 | Signaturprüfung DAF nicht durchgeführt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Hardwarereferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vorhanden oder nicht vollständig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vorhanden oder nicht vollständig |
| 0x10 | Reserviert fuer BMW |
| 0x80 | Reserviert fuer Zulieferer |
| 0xXY | unbekannter Programmierstatus |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 10 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x01 | ERROR_MISSING_BYTE1 |
| 0x02 | ERROR_VARIANT_NOT_KNOWN |
| 0x03 | ERROR_MISSING_VARIANT_BYTE |
| 0x04 | ERROR_PROGRAMMING_DATE_LENGTH |
| 0x05 | ERROR_MISSING_PROGRAMMING_DATE |
| 0x06 | ERROR_ZB_NR_LENGTH |
| 0x07 | ERROR_MISSING_ZB_NR |
| 0x08 | ERROR_MISSING_L4969_REGISTER |
| 0x09 | ERROR_MISSING_DESIRED_WINDOW |
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

Dimensions: 57 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9C5E | DRUCK SENSOR |
| 0x9C69 | FONDSCHICHTUNGSPOTI |
| 0xA6C8 | HECKSCHEIBENHEIZUNG_RELAIS |
| 0xA6C9 | WISCHER_FRONT_BLOCKIERT |
| 0xA6CA | WISCHER_STUFE_1_RELAIS |
| 0xA6CB | WISCHER_STUFE_2_RELAIS |
| 0xA6CC | SRA_RELAIS |
| 0xA6CD | WISCHER_HECK_BLOCKIERT |
| 0xA6CE | WISCHER_HECK_RELAIS |
| 0xA6CF | AUC_SENSOR |
| 0xA6D0 | KOMPRESSORVENTIL |
| 0xA6D1 | ZUSATZWASSERPUMPE |
| 0xA6D2 | WASSERVENTIL |
| 0xA6D3 | WASCHEN_FRONT |
| 0xA6D4 | ZV_ENTRIEGELN_RELAIS |
| 0xA6D5 | ZV_VERRIEGELN_RELAIS |
| 0xA6D6 | ZV_SICHERN_RELAIS |
| 0xA6D7 | ZV_VERRIEGELN_FT_RELAIS |
| 0xA6D8 | FH_BEIFAHRER_HINTEN_ZU_RELAIS |
| 0xA6D9 | FH_BEIFAHRER_HINTEN_AUF_RELAIS |
| 0xA6DA | FH_FAHRER_HINTEN_ZU_RELAIS |
| 0xA6DB | FH_FAHRER_HINTEN_AUF_RELAIS |
| 0xA6DC | WASCHEN_HECK |
| 0xA6DD | SONNENROLLO_LADERAUM |
| 0xA6DE | AUSSENSPIEGEL_HEIZUNG_LINKS |
| 0xA6DF | AUSSENSPIEGEL_HEIZUNG_RECHTS |
| 0xA6E0 | SITZHEIZUNG_FAHRER |
| 0xA6E1 | SITZHEIZUNG_BEIFAHRER |
| 0xA6E2 | ZV_ANTRIEB_HECKKLAPPE |
| 0xA6E3 | ZV_ANTRIEB_HECKSCHEIBE |
| 0xA6E4 | SENSOR_TANK_LINKS |
| 0xA6E5 | SENSOR_TANK_RECHTS |
| 0xA6E6 | SCHALTER_FH_BEIFAHRER_VORNE |
| 0xA6E7 | Energiesparmode aktiv |
| 0xA728 | SCHALTER_FH_BEIFAHRER_HINTEN |
| 0xA729 | SCHALTER_FH_FAHRER_HINTEN |
| 0xA72A | HALLSENSOR1_FH_FA_HINTEN |
| 0xA72B | HALLSENSOR2_FH_FA_HINTEN |
| 0xA72C | HALLSENSOR1_FH_BF_HINTEN |
| 0xA72D | HALLSENSOR2_FH_BF_HINTEN |
| 0xC904 | K_CAN_LOW_LEITUNG |
| 0xC905 | K_CAN_HIGH_LEITUNG |
| 0xC907 | K_CAN_KOMMUNIKATION |
| 0xC90B | PT_CAN_KOMMUNIKATION |
| 0xC910 | K_CAN_ID246_STATUSKLIMA_TIMEOUT |
| 0xC911 | K_CAN_ID246_KOMPRESSORVENTIL_UNGUELT |
| 0xC912 | K_CAN_ID246_HECKSCHHEIZUNG_UNGUELT |
| 0xC913 | K_CAN_ID246_ZUSWASSERPUMP_UNGUELT |
| 0xC914 | PT_CAN_ID2A6_BEDIENUNG_WISCHER_TIMEOUT |
| 0xC915 | PT_CAN_ID1B6_WASSERVENTIL_TIMEOUT |
| 0xC916 | PT_CAN_ID1B6_WASSERV_UNGUELT |
| 0xC918 | K_CAN_ID1E7_SITZHEIZUNG_FA_UNGUELT |
| 0xC91A | K_CAN_ID1E7_SITZHEIZUNG_BF_UNGUELT |
| 0xC91B | PT_CAN_IDB5_DREHMOMENT_EGS_TIMEOUT |
| 0xA731 | BI-Stabiles Relais |
| 0xA6E8 | ZV_WIEDERHOLSPERRE |
| 0xFFFF | unbekannter Fehlerort |

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
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Geschwindigkeit | km/h | - | unsigned int | - | 1 | 10 | 0 |
| 0x02 | BatterieSpannung | volt | - | unsigned int | - | 6675 | 240640 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 6 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC801 | ERR_SWITCH_OFF_SVAUS |
| 0xC802 | ERR_SWITCH_OFF_WAKEUP |
| 0xC803 | ERR_SWITCH_OFF_NOT_SLEEP |
| 0xC804 | ERR_MODULE_RESET |
| 0xC805 | ERR_KL30GF_POWERDOWN |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | ja |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 2 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xC805 | 0x04 | 0x03 | - | - |
| default | 0x01 | 0x02 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Geschwindigkeit | km/h | - | unsigned int | - | 1 | 10 | 0 |
| 0x02 | BatterieSpannung | volt | - | unsigned int | - | 6675 | 240640 | 0 |
| 0x03 | NM-Address | nm_id | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | RelativeZeit | s | - | signed long | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-energysaving"></a>
### ENERGYSAVING

Dimensions: 5 rows × 3 columns

| E_MODE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | ENERGY_MODE_AUS | Energysparmode aus |
| 0x01 | ENERGY_MODE_PRODUCTION | Produktionsmode ein |
| 0x02 | ENERGY_MODE_SHIPMENT | Transportmode ein |
| 0x04 | ENERGY_MODE_REPAIR_SHOP | Werkstattmode ein |
| 0x08 | ERROR | falscher Eingabewert |

<a id="table-digitalinputnrtexte"></a>
### DIGITALINPUTNRTEXTE

Dimensions: 11 rows × 4 columns

| DINNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | HECKKLAPPE_TASTER | Schalter Heckklappe aussen   .PIN 60, PORT P2.11 | Keine Betätigung: 0, Taster Gedrückt: 1 |
| 0x01 | HECKSCHEIBE_TASTER | schalter Hesckscheibe aussen .PIN 61, PORT P2.12 | Keine Betätigung: 0, Taster Gedrückt: 1 |
| 0x02 | HECKKLAPPE_KONTAKT | Kontakt Heckklappe           .PIN 62, PORT P2.13 | Geschlossen: 0, Offen: 1 |
| 0x03 | HECKSCHEIBE_KONTAKT | Kontakt Heckscheibe         .PIN 63, PORT P2.14 | Geschlossen: 0, Offen: 1 |
| 0x04 | FRONTWISCHER_RSK | Parkposition Frontwischer  .ShiftRegisterSwitch.1 | FrontWischer nicht im RSK: 0, FrontWischer im RSK: 1 |
| 0x05 | HECKWISCHER_RSK | Parkposition Heckwischer   .ShiftRegisterSwitch.2 | HeckWischer nicht im RSK: 0, HeckWischer im RSK: 1 |
| 0x06 | DSC_BEFEHL | Sensor DSC schalter          .ShiftRegisterSwitch.3 | Taster Gedrückt: 0,Keine Betätigung: 1 |
| 0x07 | KUEHLMITTELSTAND | Sensor Kuehlmittelstand       .ShiftRegisterSwitch.5 | Zu niedrigem Füllstand: 0, Normales Füllstand: 1 |
| 0x08 | WASCHWASSERSTAND | Sensor Waschwasser         .ShiftRegisterSwitch.6 | Zu niedrigem Füllstand: 0, Normales Füllstand: 1 |
| 0x09 | HANDBREMSE_KONTAKT | Eingang Schalter Handbremse     .ShiftRegisterSwitch.7 | Gelöst: 0, Angezogen: 1 |
| 0xFF | UNKNOWN | unbekannte Digital Input |  |

<a id="table-digitaloutputnrtexte"></a>
### DIGITALOUTPUTNRTEXTE

Dimensions: 52 rows × 4 columns

| DOUTNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | AUCSENSOR_ENABLE | AUC Sensor aktiv                    .PIN 1,PORT P6.0 | DISABLE: 0, ENABLE: 1 |
| 0x01 | EEPROM_ENABLE | EEprom freigegeben                        .PIN 2,PORT P6.1 | ENABLE: 0, DISABLE: 1 |
| 0x02 | KL30SW_ENABLE | KL30SW freigegeben                        .PIN 3,PORT P6.2 | DISABLE: 0, ENABLE: 1 |
| 0x03 | 5V_SENSOR_ENABLE | 5V SENSOR freigegeben                     .PIN 4,PORT P6.3 | DISABLE: 0, ENABLE: 1 |
| 0x04 | SHIFTREGISTER_CONTROL | Shift Register Control               .PIN 5,PORT P6.4 | OFF: 0, ON: 1 |
| 0x05 | SHIFTREGISTER_CLOCK | Shift Register Clock                 .PIN 6,PORT P6.5 | LOW: 0, HIGH: 1 |
| 0x06 | FRONTWASCHERPUMPE | Waschpumpe vorne                    .PIN 10,PORT P8.1 | AUS: 0, EIN: 1 |
| 0x07 | HECKWASCHERPUMPE | Waschpumpe hinten                     .PIN 12,PORT P8.3 | AUS: 0, EIN: 1 |
| 0x08 | SONNENROLLO_AUSGANG | Ausgang Sonnenrollo | AUS: 0, Von EIN zu AUS: 5, NACH OBEN: 6, HERUNTER: 9 |
| 0x09 | SONNENROLLO_LOWTREIBER1 | Sonnenrollo Mosfet LowSide  1           .PIN 13,PORT P8.4 | OFF: 0, ON: 1 |
| 0x0A | SONNENROLLO_HIGHTREIBER1 | Sonnenrollo Mosfet HighSide 1           .PIN 14,PORT P8.5 | OFF: 0, ON: 1 |
| 0x0B | SONNENROLLO_LOWTREIBER2 | Sonnenrollo Mosfet LowSide  2           .PIN 15,PORT P8.6 | OFF: 0, ON: 1 |
| 0x0C | SONNENROLLO_HIGHTREIBER2 | Sonnenrollo Mosfet HigSide  2           .PIN 16,PORT P8.7 | OFF: 0, ON: 1 |
| 0x0D | TANKSENSOREN_ENABLE | Tank                            .PIN 24,PORT P7.5 | DISABLE: 0, ENABLE: 1 |
| 0x0E | SERIALCOM_VR_OUT | Datenausgang zu Spannungsregler        .PIN 52,PORT P2.5 | OFF: 0, ON: 1 |
| 0x0F | SERIALCOM_VR_CLOCK | Ausgang Clock Spannungsregler       .PIN 53,PORT P2.6 | LOW: 0, HIGH: 1 |
| 0x10 | CONTACTWAKE_IN_ENABLE | WakeUp-Kontakt freigegeben                 .PIN 57,PORT P2.8 | DISABLE: 0, ENABLE: 1 |
| 0x11 | WASCHDUESENHEIZUNG_AUßENSPIEGEL_AUSGANG | Ausgang Waschduesenheizung | AUS: 0, Rechts EIN: 1, Links EIN: 2, Beides EIN: 3 |
| 0x12 | WASCHDUESENHEIZUNG_AUßENSPIEGEL_RECHTS | Waschduesenheizung rechts              .PIN 70,PORT P3.5 | OFF: 0, ON: 1 |
| 0x13 | WASCHDUESENHEIZUNG_AUßENSPIEGEL_LINKS | Waschduesenheizung links               .PIN 73,PORT P3.6 | OFF: 0, ON: 1 |
| 0x14 | PTWAKE_OUT | PT CAN Wake UP                       .PIN 74,PORT P3.7 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x15 | SPI_OUTPUT | SPI Data Out                         .PIN 76,PORT P3.9 | LOW: 0, HIGH: 1 |
| 0x16 | TX_DIAG | Diagnostic TX                        .PIN 77,PORT P3.10 | LOW: 0, HIGH: 1 |
| 0x17 | SPI_CLOCK | SPI Data Clock                       .PIN 80,PORT P3.13 | LOW: 0, HIGH: 1 |
| 0x18 | ZUSATZWASSERPUMPE | Zusatzwasserpumpe                .PIN 86,PORT P4.1 | AUS: 0, EIN: 1 |
| 0x19 | FH_CHIPSELECT | el. Fensterheber Chip Select              .PIN 87,PORT P4.2 | DISABLE: 0, ENABLE: 1 |
| 0x1A | HIGHSPEEDCAN_ENABLE | High Speed CAN Enable                .PIN 88,PORT P4.3 | ENABLE: 0, DISABLE: 1 |
| 0x1B | HIGHSPEEDCAN_TX | High Speed CAN TX                    .PIN 91,PORT P4.6 | LOW: 0, HIGH: 1 |
| 0x1C | LOWSPEEDCAN_TX | Low Speed CAN TX                     .PIN 92,PORT P4.7 | LOW: 0, HIGH: 1 |
| 0x1D | FH_BFTH_AUSGANG | Ausgang el. Fensterheber Beifahrer hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x1E | FH_BFTH_AUF | OPENRELAIS el. Fensterheber Beifahrer hinten  .PIN 118,PORT P1L.0 | OFF: 0, ON: 1 |
| 0x1F | FH_BFTH_ZU | CLOSERELAIS el. Fensterheber Beifahrer hinten .PIN 119,PORT P1L.1 | OFF: 0, ON: 1 |
| 0x20 | FH_FATH_AUSGANG | Ausgang el. Fensterheber Fahrer hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x21 | FH_FATH_AUF | OPENRELAIS el. Fensterheber Fahrer hinten     .PIN 120,PORT P1L.2 | OFF: 0, ON: 1 |
| 0x22 | FH_FATH_ZU | CLOSERELAIS el. Fensterheber Fahrer hinten    .PIN 121,PORT P1L.3 | OFF: 0, ON: 1 |
| 0x23 | FH_BFTH_AUSGANG & FH_FATH_AUSGANG | Ausgang el. Fensterheber Fahrer und Beifahrer hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x24 | HECKWISCHER | Relais Heckwischer                      .PIN 122,PORT P1L.4 | AUS: 0, EIN: 1 |
| 0x25 | FRONTWISCHER_AUSGANG | Ausgang Frontwischer | AUS: 0, Stufe1: 1,Stufe2: 3 |
| 0x26 | FRONTWISCHER | Relais Frontwischer                     .PIN 123,PORT P1L.5 | OFF: 0, ON: 1 |
| 0x27 | FRONTWISCHER_GESCHW | Speed-Relais Frontwischer               .PIN 124,PORT P1L.6 | OFF: 0, ON: 1 |
| 0x28 | SRA | Relais ScheinwerferReinigungsAnlage (SRA)                .PIN 125,PORT P1L.7 | OFF: 0, ON: 1 |
| 0x29 | ZV_AUSGANG | Ausgang Zentralverriegelung | Aus: 0, Entriegeln: 2, Selektiv Entriegeln: 6, Verriegeln: 12, Sichern: 13, Entsichern: 14 |
| 0x2A | ZV_SICHERN_RELAIS | Relais Sicherung Zentralverriegelung           .PIN 128,PORT P1H.0 | OFF: 0, ON: 1 |
| 0x2B | ZV_ENTRIEGELN_RELAIS | Relais Entriegelung Zentralverriegelung           .PIN 129,PORT P1H.1 | OFF: 0, ON: 1 |
| 0x2C | ZV_VERRIEGELN_RELAIS | Relais Verriegelung Zentralverriegelung             .PIN 130,PORT P1H.2 | OFF: 0, ON: 1 |
| 0x2D | ZV_SELEKTIV_VERRIEGELN_RELAIS | Relais Verriegelung Fahrer Zentralverriegelung       .PIN 131,PORT P1H.3 | OFF: 0, ON: 1 |
| 0x2E | HECKKLAPPE | Relais Heckklappe                       .PIN 132,PORT P1H.4 | AUS: 0, EIN: 1 |
| 0x2F | HECKSCHEIBE | Relais Heckscheibe                     .PIN 133,PORT P1H.5 | AUS: 0, EIN: 1 |
| 0x30 | HECKSCHEIBENHEIZUNG | Relais Heckscheibenheizung              .PIN 134,PORT P1H.6 | AUS: 0, EIN: 1 |
| 0x31 | BISTABILRELAIS_ON | BI-Stabiles Relais an                   .PIN 135,PORT P1H.7 | AUS: 0, EIN: 1 |
| 0x32 | BISTABILRELAIS_OFF | BI-Stabiles Relais aus                  .PIN 85 ,PORT P4.0 | AUS: 0, EIN: 1 |
| 0xFF | UNKNOWN | unbekannte Digital Output |   |

<a id="table-analoginputnrtexte"></a>
### ANALOGINPUTNRTEXTE

Dimensions: 13 rows × 4 columns

| AINNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | KOMPRESSORVENTIL_STROM | StromSensor Kompressor          .PIN 27,PORT P5.0 | 0...0x3FF(1023) |
| 0x01 | DRUCKSENSOR | Drucksensor                    .PIN 28,PORT P5.1 | Gültig:0x052(82)(0 Bar)...0x3AD(941)(35 Bar): (PH)=(((HEX)-0.4*(1023/5))*35)/859  [bar] |
| 0x02 | FH_BFT_SCHALTER | Taster el. Fensterheber Beifahrer       .PIN 29,PORT P5.2 | 143(0x08F)......346(0x15A) : DOWNAUTO(2), 347(0x15B)....571(0x23B) : DOWNMANUAL(1), 572(0x23C)....756(0x2F4) : UPAUTO(4), 757(0x2F5)....951(0x3B7) : UPMANUAL(3), 952(0x3B8)....1023(0x3FF): OFF(0) |
| 0x03 | FH_FATH_SCHALTER | Taster el. Fensterheber Fahrer hinten     .PIN 30,PORT P5.3 | 143(0x08F)......346(0x15A) : DOWNAUTO(2), 347(0x15B)....571(0x23B) : DOWNMANUAL(1), 572(0x23C)....756(0x2F4) : UPAUTO(4), 757(0x2F5)....951(0x3B7) : UPMANUAL(3), 952(0x3B8)....1023(0x3FF): OFF(0) |
| 0x04 | FH_BFTH_SCHALTER | Taster el. Fensterheber Beifahrer hinten  .PIN 31,PORT P5.4 | 143(0x08F)......346(0x15A) : DOWNAUTO(2), 347(0x15B)....571(0x23B) : DOWNMANUAL(1), 572(0x23C)....756(0x2F4) : UPAUTO(4), 757(0x2F5)....951(0x3B7) : UPMANUAL(3), 952(0x3B8)....1023(0x3FF): OFF(0) |
| 0x05 | TANK_FA_FUELLSTAND | Tankgeber links                   .PIN 32,PORT P5.5 | 0...0x3FF(1023) |
| 0x06 | TANK_BF_FUELLSTAND | Tankgeber rechts                .PIN 33,PORT P5.6 | 0...0x3FF(1023) |
| 0x07 | FH_BFTH_STROM | Strom el. Fensterheber Beifahrer hinten .PIN 34,PORT P5.7 | 0(0 A)...0x3FF(1023)(39 A): (PH)=((HEX)*39)/1024  [A] |
| 0x08 | FH_FATH_STROM | Strom el. Fensterheber Fahrer hinten    .PIN 35,PORT P5.8 | 0(0 A)...0x3FF(1023)(39 A): (PH)=((HEX)*39)/1024  [A] |
| 0x09 | FONDSCHICHTUNGSENSOR | Fondschichtungssensor aktivieren       .PIN 36,PORT P5.9 | Gültig:0x133(307)(0 %)...0x2B8(696)(100 %): (PH)=(((HEX)-1.5*(1023/5))*100)/389  [%] |
| 0x0A | SONNENROLLO_STROM | Sonnenrollo Strom Sensor           .PIN 39,PORT P5.10 | 0...0x3FF(1023) |
| 0x0B | BATTERIE_SPANNUNG | Batteriespannung                    .PIN 40,PORT P5.11 | 0(0 V)...0x3FF(1023)(28.40 V) (HEX);Vbat=(HEX)*100/3605  [V] |
| 0xFF | UNKNOWN | unbekannte Analog Output |  |

<a id="table-analogoutputnrtexte"></a>
### ANALOGOUTPUTNRTEXTE

Dimensions: 6 rows × 4 columns

| AOUTNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | KOMPRESSORVENTIL_PWM | Spannung Kompressorventil (PWM) | 0(0 %)...0x061B(1563)(100 %) |
| 0x01 | WASSERVENTIL | Wasserventil                        .PIN 20,PORT P7.1 | OFF: 0, ON: 1 |
| 0x02 | WASSERVENTIL_PWM | Spannung Wasserventil (PWM). Voraussetzungen muessen erfuellt sein | 0(0 %)...0x0168(360)(100 %) |
| 0x03 | SITZHEIZUNG_FA_PWM | Spannung Sitzheizung Fahrer (PWM) | OFF: 25000, STATE1: 20000, STATE2: 12500, STATE3: 7500 |
| 0x04 | SITZHEIZUNG_BF_PWM | Spannung Sitzheizung Beifahrer (PWM) | OFF: 25000, STATE1: 20000, STATE2: 12500, STATE3: 7500 |
| 0xFF | UNKNOWN | unbekannte Analog Output |  |

<a id="table-senseinputnrtexte"></a>
### SENSEINPUTNRTEXTE

Dimensions: 23 rows × 4 columns

| SINNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | FIVEVOLTS_SENSOR_DIAG | Diag 5V-Sensor                  .PIN 41,PORT P5.12 | 0...0x3FF(1023) |
| 0x01 | WASCHDUSENHEIZUNG_AUßENSPIEGEL_DIAG | Diag Waschduesenheizung Analog           .PIN 42,PORT P5.13 | 0...0x3FF(1023) |
| 0x02 | WASCHERPUMPE_DIAG | Diag Wasserpumpe Analog                 .PIN 43,PORT P5.14 | 0...0x3FF(1023) |
| 0x03 | WASSERVENTIL_DIAG | Diag Wasserventil Analog       .PIN 44,PORT P5.15 | 0...0x3FF(1023) |
| 0x04 | ZUSATZWASSERPUMPE_DIAG | Diag Zusatzwasserpumpe             .ShiftReg1Diagnostic.0 | Fehler: 0, In Ordnung: 1 |
| 0x05 | FRONTWISCHER_DIAG | Diag Schalter Frontwischer                .ShiftReg1Diagnostic.2 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x06 | FRONTWISCHER_GESCHW_DIAG | Diag Raendelrad Frontwischer          .ShiftReg1Diagnostic.3 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x07 | FH_FATH_AUF_DIAG | Diag el. Fensterheber Fahrer hinten OFFEN      .ShiftReg1Diagnostic.4 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x08 | FH_FATH_ZU_DIAG | Diag el. Fensterheber Fahrer hinten GESCHLOSSEN     .ShiftReg1Diagnostic.5 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x09 | FH_BFTH_AUF_DIAG | Diag el. Fensterheber Beifahrer hinten OFFEN   .ShiftReg1Diagnostic.6 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x0A | FH_BFTH_ZU_DIAG | Diag el. Fensterheber Beifahrer hinten GESCHLOSSEN  .ShiftReg1Diagnostic.7 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x0B | HECKWISCHER_DIAG | Diag Heckwischer                        .ShiftReg2Diagnostic.0 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x0C | SRA_DIAG | Diag ScheinwerferReinigungsAnlage                   .ShiftReg2Diagnostic.1 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x0D | ZV_VERRIEGELN_RELAIS_DIAG | Diag Relais Zentralveriegelung verriegeln        .ShiftReg2Diagnostic.2 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x0E | ZV_ENTRIEGELN_RELAIS_DIAG | Diag Relais Zentralveriegelung entriegeln      .ShiftReg2Diagnostic.3 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x0F | ZV_SICHERN_RELAIS_DIAG | Diag Relais Zentralveriegelung sichern      .ShiftReg2Diagnostic.4 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x10 | HECKSCHEIBENHEIZUNG_DIAG | Diag Heckscheibenheizung                 .ShiftReg2Diagnostic.5 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x11 | ZV_SELEKTIV_ENTRIEGELN_RELAY_DIAG | Diag Relais Zentralveriegelung verriegeln Fahrer  .ShiftReg2Diagnostic.6 | Relais Abgeschaltet: 0, Relais Eingeschaltet: 1 |
| 0x12 | SITZHEIZUNG_BF_DIAG | Diag Sitzheizung Beifahrer            .PIN 47,PORT P2.0 | Ausgang Nicht Aktiv: 0, Ausgang Aktiv: 1 |
| 0x13 | SITZHEIZUNG_FA_DIAG | Diag Sitzheizung Fahrer               .PIN 59,PORT P2.10 | Ausgang Nicht Aktiv: 0, Ausgang Aktiv: 1 |
| 0x14 | HECKKLAPPE_DIAG | Diag Heckklappe                         .PIN 65,PORT P3.0 | In Ordnung: 0, Fehler: 1 |
| 0x15 | HECKSCHEIBE_DIAG | Diag Heckscheibe                       .PIN 66,PORT P3.1 | In Ordnung: 0, Fehler: 1 |
| 0xFF | UNKNOWN | unbekannte Sense Input |  |

<a id="table-funktionaleadresse"></a>
### FUNKTIONALEADRESSE

Dimensions: 8 rows × 3 columns

| NR | F_ADR | F_ADR_TEXT |
| --- | --- | --- |
| 0xE9 | K-CAN | Karosserie-CAN Steuergeräte |
| 0xEA | PT-CAN | Powertrain-CAN Steuergeräte |
| 0xEB | SI | Sicherheits-BUS Steuergeräte |
| 0xEC | MOST | MOST-BUS Steuergeräte |
| 0xED | BOS | Bedarfsorientierter Service |
| 0xED | CBS | Bedarfsorientierter Service |
| 0xEE | PERSONAL | Personalisierung |
| 0xEF | ALL | alle Steuergeräte |

<a id="table-initapinch"></a>
### INITAPINCH

Dimensions: 7 rows × 3 columns

| NR | AUSWAHL_FH | MODE_TEXT |
| --- | --- | --- |
| 0x01 | FAH | FahrerTür Hinten |
| 0x02 | BFH | BeifahrerTür Hinten |
| 0x03 | BEIDE | Beide |
| 0x01 | 0 | FahrerTür Hinten |
| 0x02 | 1 | BeifahrerTür Hinten |
| 0x03 | 2 | Beide |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-learningresult"></a>
### LEARNINGRESULT

Dimensions: 3 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x01 | JA |
| 0x00 | NEIN |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-unnormapinch"></a>
### UNNORMAPINCH

Dimensions: 7 rows × 3 columns

| NR | AUSWAHL_FH | MODE_TEXT |
| --- | --- | --- |
| 0x05 | FAH | FahrerTür Hinten |
| 0x06 | BFH | BeifahrerTür Hinten |
| 0x07 | BEIDE | Beide |
| 0x05 | 0 | FahrerTür Hinten |
| 0x06 | 1 | BeifahrerTür Hinten |
| 0x07 | 2 | Beide |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-steuernrearwindows"></a>
### STEUERNREARWINDOWS

Dimensions: 10 rows × 4 columns

| SRWNR | AUSWAHL_FH | MODE_TEXT | WERT |
| --- | --- | --- | --- |
| 0x1D | BFH | BeifahrerTür Hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x20 | FAH | FahrerTür Hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x23 | BEIDE | Beide | AUS: 0, AUF: 1, ZU: 2 |
| 0x1D | 0 | BeifahrerTür Hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x20 | 1 | FahrerTür Hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x23 | 2 | Beide | AUS: 0, AUF: 1, ZU: 2 |
| 0x1D | 0x00 | BeifahrerTür Hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x20 | 0x01 | FahrerTür Hinten | AUS: 0, AUF: 1, ZU: 2 |
| 0x23 | 0x02 | Beide | AUS: 0, AUF: 1, ZU: 2 |
| 0xFF | -- | unbekannter Diagnose-Mode |  |

<a id="table-variant-table"></a>
### VARIANT_TABLE

Dimensions: 7 rows × 3 columns

| VARIANT_NUMBER | VARIANT_BYTE | VARIANT_NAME |
| --- | --- | --- |
| 0x00 | LOW1 | LOW1   ohne WI/WA Heck, ohne FH, ohne Sonnenrollo |
| 0x01 | LOW2 | LOW2   mit WI/WA Heck, ohne FH, ohne Sonnenrollo |
| 0x02 | HIGH1 | HIGH1  ohne WI/WA Heck, mit FH, ohne Sonnenrollo |
| 0x03 | HIGH2 | HIGH2  mit WI/WA Heck, mit FH, ohne Sonnenrollo |
| 0x04 | HIGH3 | HIGH3  ohne WI/WA Heck, mit FH, mit Sonnenrollo |
| 0x05 | HIGH4 | HIGH4  mit WI/WA Heck, mit FH, mit Sonnenrollo/Laderaumabdeckung |
| 0xXY | -- | -- |
