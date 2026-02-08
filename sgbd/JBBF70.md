# JBBF70.prg

- Jobs: [136](#jobs)
- Tables: [47](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | JBBF2 |
| ORIGIN | BMW EI-61 Philipp Neumeyer |
| REVISION | 1.001 |
| AUTHOR | Lear Corporation Entwicklung Arseni Martínez, Lear Corporation Entwicklung Carme Tàpias, Lear Corporation Entwicklung Israel Revert, Lear Corporation Entwicklung Sergi Garriga |
| COMMENT | SGBD of JBBFE2 for E70 |
| PACKAGE | 1.31 |
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
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [STEUERN_MEMORIES_LOESCHEN](#job-steuern-memories-loeschen) - Delete FZM memories (SOLL, IST, secondary, primary) KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific
- [STEUERN_WECKRINGSPEICHER_LOESCHEN](#job-steuern-weckringspeicher-loeschen) - Delete waking registration memory KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE8 commonProjectSpecific
- [STATUS_WECKRINGSPEICHER_LESEN](#job-status-weckringspeicher-lesen) - Reads waking registration memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE9 commonProjectSpecific
- [STATUS_PRIMAERSPEICHER_FZM_LESEN](#job-status-primaerspeicher-fzm-lesen) - Reads primary control memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE6 commonProjectSpecific
- [STATUS_SEKUNDAERSPEICHER_FZM_LESEN](#job-status-sekundaerspeicher-fzm-lesen) - Read secondary control memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE7 commonProjectSpecific
- [STATUS_SOLLSTAND_FZM_LESEN](#job-status-sollstand-fzm-lesen) - Reads ISTDATEN memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE5 commonProjectSpecific
- [STATUS_ISTSTAND_FZM_LESEN](#job-status-iststand-fzm-lesen) - Reads ISTDATEN memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE4 commonProjectSpecific
- [READ_ENERGY_SAVING_MODE](#job-read-energy-saving-mode) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [_READ_MEMORY_BY_ADDRESS](#job-read-memory-by-address) - Selected MEMORY reading by Address KWP 2000: $23  ReadMemoryByAddress KWP 2000: $02  External EEPROM KWP 2000: $04  Internal RAM
- [_WRITE_MEMORY_BY_ADDRESS](#job-write-memory-by-address) - Selected MEMORY writing by Address KWP 2000: $3D  WriteMemoryByAddress KWP 2000: $02  External EEPROM KWP 2000: $04  Internal RAM
- [_READ_DISP_EE](#job-read-disp-ee) - Read EEPROM EE Struct and Disp Flags KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C000 commonProjectSpecific
- [_WRITE_DISP_EE](#job-write-disp-ee) - Write EEPROM EE Struct and Disp Flags KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFFF commonProjectSpecific
- [_READ_BRIF](#job-read-brif) - Lear specific Job for reading BRIF from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C001 commonProjectSpecific
- [_READ_ZIF](#job-read-zif) - Lear specific Job for reading ZIF from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C002 commonProjectSpecific
- [_READ_LENGTH_DIAG_BUFFER](#job-read-length-diag-buffer) - Read Diag Buffer Lenth KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C003 commonProjectSpecific
- [STATUS_VERSION_GATEWAYMODULES](#job-status-version-gatewaymodules) - Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6F RecordLocalId Modus  : Default
- [_STATUS_VERSION_GATEWAY_FILES](#job-status-version-gateway-files) - Lesen der Versionsnummer der Gateway software Dateien KWP2000: $21 ReadDataByLocalIdentifier $6A RecordLocalId Modus  : Default
- [STEUERN_FENSTERHEBER_DENORMIEREN](#job-steuern-fensterheber-denormieren) - Denormiert gewählten Fensterheber Denormalize selected Window KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $00 FH denormieren
- [STEUERN_FENSTERHEBER_EINLERNEN_OHNE_EKS](#job-steuern-fensterheber-einlernen-ohne-eks) - Normiert gewählten Fensterheber (ohne EKS) Normalize selected Window (without Apinch) Dauer max. 5 sec KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $01 Einlernen der Fensterheber
- [STEUERN_FENSTERHEBER_EINLERNEN](#job-steuern-fensterheber-einlernen) - Einlernen der Fensterheber Normiert gewaehlten Fensterheber (mit EKS) Normalize selected Window (with Apinch) Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen Ob Einlernvorgang noch laeuft ist ueber: Job: STATUS_TUER Result: STAT_FH_*_EINLERNENVORGANG_AKTIV abrufbar. Ob ein Fenster eingelernt ist ueber: Result: STAT_FH_*_EINGELERNT KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH EKS JOBS $07 ShortTermAdjustment $02 Hublaenge zum Einlernen aus Codierdaten lesen und Einlernen starten
- [STATUS_FENSTERHEBER_HINTEN](#job-status-fensterheber-hinten) - Gibt aktuellen Zustand Fensterheber wieder Status Rear Windows (z.B. Position, Normierung, Verfahrrichtung, etc) KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $03 Stati der Fensterheber fuer JBBFE2
- [STEUERN_FENSTERHEBER_HINTEN](#job-steuern-fensterheber-hinten) - Verfaehrt gewaehlten Fensterheber gemaeß Control Rear Windows angegebener Richtung und Zeit (ms) KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $04 Ansteuern FH
- [STATUS_FH_LOGGER_DENORMIERER](#job-status-fh-logger-denormierer) - Fensterheber Denormierungslogger auslesen Lesen von EE_FH_LOG_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $05 EE_FH_LOG_DATA Status
- [_STATUS_FH_LOGGER_DENORMIERER_LEAR](#job-status-fh-logger-denormierer-lear) - Fensterheber Denormierungslogger auslesen Lesen von EE_FH_LOG_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $05 EE_FH_LOG_DATA Status
- [STEUERN_FH_LOGGER_DENORMIERER](#job-steuern-fh-logger-denormierer) - Denormierungslogger löschen Loeschen von EE_FH_LOG_DATA des jbbfe2 KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $05 EE_FH_LOG_DATA Loeschen
- [STATUS_FH_LOGGER_REVERSIERER](#job-status-fh-logger-reversierer) - Fensterheber Reversierlogger auslesen Lesen von EE_FH_REV_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $08 EE_FH_REV_DATA Status
- [_STATUS_FH_LOGGER_REVERSIERER_LEAR](#job-status-fh-logger-reversierer-lear) - Fensterheber Reversierlogger auslesen Lesen von EE_FH_REV_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $08 EE_FH_REV_DATA Status
- [STEUERN_FH_LOGGER_REVERSIERER](#job-steuern-fh-logger-reversierer) - Reversierungslogger löschen Loeschen von EE_FH_REV_DATA des jbbfe2 KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH BROSE JOBS $07 ShortTermAdjustment $08 EE_FH_REV_DATA Loeschen
- [STEUERN_FENSTERHEBER_MESSDATEN_AKTIVIEREN](#job-steuern-fensterheber-messdaten-aktivieren) - Messdatenausgabe fuer FH starten KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $06 MESSDATEN_AKTIVIEREN
- [STATUS_QUALITAET_FENSTERHEBERLAUF](#job-status-qualitaet-fensterheberlauf) - Qualitaetsbewertung Fensterheber Fensterheber muss eingelernt sein und mind. einmalig mit Panikoption = 1 verfahren worden sein KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $XX XX
- [_STATUS_FH_ADAPTIONSSPEICHER_LESEN](#job-status-fh-adaptionsspeicher-lesen) - Adaptionsdaten Fensterheber KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $07 ECHT_ZEIT_DATEN
- [STEUERN_FH_ADAPTIONSSPEICHER_LOESCHEN](#job-steuern-fh-adaptionsspeicher-loeschen) - Adaptionsdaten Fensterheber Loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $0E ECHT_ZEIT_DATEN ZONE 4 Loeschen
- [_ECHTZEITDATEN_BROSE_LESEN](#job-echtzeitdaten-brose-lesen) - Echtzeitdaten vom Brose auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $07 ECHT_ZEIT_DATEN
- [_STEUERN_DIAGNOSE_BROSE_FH_1](#job-steuern-diagnose-brose-fh-1) - Status von JBBFE2 schreiben KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $09 Diagnose fuer BROSE-FH
- [_STATUS_FH_EKS_CODDATA](#job-status-fh-eks-coddata) - Coding EKS BROSE reading from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $3500-0x350F commonProjectSpecific
- [_STEUERN_FH_EKS_CODDATA](#job-steuern-fh-eks-coddata) - Coding EKS BROSE writing to EEPROM and RAM KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $3500-0x350F commonProjectSpecific
- [_SLEEP_MODE_FUNKTIONAL](#job-sleep-mode-funktional) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default
- [_SLEEP_MODE_LEAR](#job-sleep-mode-lear) - Send ECU to Sleep Mode without waiting the busses to stop KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $02 Specific Lear Modus  : Default
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_1](#job-status-historienspeicher-lesen-block-1) - EnergieDatenSpeicher Teil 1 -Einschlafverhinderer- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE1 commonProjectSpecific
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_2](#job-status-historienspeicher-lesen-block-2) - EnergieDatenSpeicher Teil 2 -Wecker- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_3](#job-status-historienspeicher-lesen-block-3) - EnergieDatenSpeicher Teil e -Wecker IDs- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE3 commonProjectSpecific
- [STATUS_HISTORIENSPEICHER_LESEN_DETAIL_BLOCK_3](#job-status-historienspeicher-lesen-detail-block-3) - EnergieDatenSpeicher Teil e -Wecker IDs- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE3 commonProjectSpecific
- [STEUERN_HISTORIENSPEICHER_LOESCHEN](#job-steuern-historienspeicher-loeschen) - EnergieDatenSpeicher Teil 1 TEIL 2 und Teil 3 loeschen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE0 commonProjectSpecific
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Inputs $01 ReportCurrentState
- [STATUS_DIGITAL_OUTPUTS](#job-status-digital-outputs) - Auslesen der Stati von den digitalen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Outputs $01 ReportCurrentState
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Inputs $01 ReportCurrentState
- [STATUS_ANALOG_OUTPUTS](#job-status-analog-outputs) - Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Outputs $01 ReportCurrentState
- [STEUERN_DIGITAL_INPUT](#job-steuern-digital-input) - Digitale Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $07 ShortTermAdjustment
- [STEUERN_DIGITAL_OUTPUT](#job-steuern-digital-output) - Digitale Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Ouput $07 ShortTermAdjustment
- [STEUERN_ANALOG_INPUT](#job-steuern-analog-input) - Analoge Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Input $07 ShortTermAdjustment
- [STEUERN_ANALOG_OUTPUT](#job-steuern-analog-output) - Analoge Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Output $07 ShortTermAdjustment
- [STEUERN_BEENDEN](#job-steuern-beenden) - Kontrolle an JBBFE zurueckgeben KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $02 Digitale Output $03 Analoge Input $04 Analoge Output $00 ReturnControToECU
- [_STATUS_VAR_IAP_WWS_ASCET_INPUT](#job-status-var-iap-wws-ascet-input) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $00 Wiper/Washer System Ascet Model $00 Input Variables
- [_STATUS_VAR_IAP_WWS_ASCET_OUTPUT](#job-status-var-iap-wws-ascet-output) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $00 Wiper/Washer System Ascet Model $01 Output Variables
- [_STATUS_VAR_IAP_WWS_ASCET_COD](#job-status-var-iap-wws-ascet-cod) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $00 Wiper/Washer System Ascet Model $02 Coding Variables
- [_STATUS_VAR_IAP_PWR_ASCET_INPUT](#job-status-var-iap-pwr-ascet-input) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $01 Power Window Ascet Model $00 Input Variables
- [_STATUS_VAR_IAP_PWR_ASCET_OUTPUT](#job-status-var-iap-pwr-ascet-output) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $01 Power Window Ascet Model $01 Output Variables
- [_STATUS_VAR_IAP_PWR_ASCET_COD](#job-status-var-iap-pwr-ascet-cod) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $01 Power Window Ascet Model $02 Coding Variables
- [_STATUS_VAR_CAN_PWR](#job-status-var-can-pwr) - Auslesen der Stati von den Fensterheber CAN Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 CAN Variables $01 ReportCurrentState $08 PWR
- [_STATUS_VAR_IAP_PWR](#job-status-var-iap-pwr) - Auslesen der Stati von den Fnesterheber Internal Varablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $08 PWR
- [_STATUS_VAR_IAP_FZM](#job-status-var-iap-fzm) - Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $09 FZM
- [_STATUS_VAR_IAP_ATMEL](#job-status-var-iap-atmel) - Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $0A Atmel
- [_FLASH_COMICRO](#job-flash-comicro) - Internen Flashvorgang des Co-Prozessors anstossen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE4 commonProjectSpecific
- [_STATUS_COMICRO](#job-status-comicro) - KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C200 commonProjectSpecific
- [_LEAR_PLx_EOL_CONFIGURATION](#job-lear-plx-eol-configuration) - Configuration for the LEAR End of Line KWP2000: $3B WriteDataByLocalIdentifier $7A RecordLocalId
- [READ_VARIANT](#job-read-variant) - Lesen der Variante der Plattine KWP2000: $21 ReadDataByLocalIdentifier $6E RecordLocalId Modus  : Default
- [STEUERN_WASCHDUESE_AUSSENSPIEGEL](#job-steuern-waschduese-aussenspiegel) - Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $79 RecordLocalId
- [_EEPROM_INIT](#job-eeprom-init) - Initialise the EEPROM KWP2000: $3B WriteDataByLocalIdentifier $7E RecordLocalId
- [AIF_LESEN_READECU](#job-aif-lesen-readecu) - Auslesen des Anwender Informations Feldes KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default
- [_DTC_ENABLE_GET](#job-dtc-enable-get) - KWP2000: $21 ReadDataByLocalIdentifier $70 RecordLocalId Returns the status of DTC_enable Cache14 2 bit / DTC 1st ..... Enabled/ Disabled 2nd ..... Protect / Unprotect Load
- [_DTC_ENABLE_SET](#job-dtc-enable-set) - Modifies EEpromCache14 (DTC enable/disable) KWP2000: $3B WriteDataByLocalIdentifier $70 RecordLocalId 2 bit / DTC 1st ..... Enabled/ Disabled 2nd ..... Protect / Unprotect Load
- [_DTC_ENABLE_ALL](#job-dtc-enable-all) - Modifies EEpromCache14 (DTC enable/disable) KWP2000: $3B WriteDataByLocalIdentifier $71 RecordLocalId Sets all DTCs for Protection
- [_DTC_DISABLE_ALL](#job-dtc-disable-all) - Modifies EEpromCache14 (DTC enable/disable) KWP2000: $3B WriteDataByLocalIdentifier $72 RecordLocalId Sets all DTCs for Protection
- [STATUS_SCHALTERBLOCK_TUER](#job-status-schalterblock-tuer) - Abfragen der Stati der angeschlossenen Schalterbloecke KWP2000: $30 InputOutputControlByLocalIdentifier $08 BAUSTEIN_TUER $01 ReportCurrentState $00 SCHALTERBLOCK_TUER
- [STATUS_TUER](#job-status-tuer) - Status-Abfragen Tuer Beinhaltet Fenster, Fensterheber, Spiegel und Zentralverriegelung KWP2000: $30 InputOutputControlByLocalIdentifier $08 BAUSTEIN_TUER $01 ReportCurrentState $01 STATUS_TUER
- [STEUERN_DIGITAL_TUER](#job-steuern-digital-tuer) - Ansteuerung der digitalen Eingaenge KWP2000: $30 InputOutputControlByLocalIdentifier $08 BAUSTEIN_TUER $07 ShortTermAdjustment $02 STEUERN_TUER
- [STEUERN_SPIEGEL_HEIZUNG](#job-steuern-spiegel-heizung) - Ein bzw. Ausschalten der Spiegelheizung per Diagnose
- [STEUERN_ZWP](#job-steuern-zwp) - Schreiben die Zussatzwasserpumpe parameter KWP2000: $3B WriteDataByLocalIdentifier $77 RecordLocalId
- [STEUERN_WASSERVENTIL_FAHRER](#job-steuern-wasserventil-fahrer) - Schreiben die Wasserventil parameter KWP2000: $3B WriteDataByLocalIdentifier $78 RecordLocalId
- [STEUERN_WASSERVENTIL_BEIFAHRER](#job-steuern-wasserventil-beifahrer) - Schreiben die Wasserventil parameter KWP2000: $3B WriteDataByLocalIdentifier $76 RecordLocalId
- [STATUS_CODIERBITS](#job-status-codierbits) - Einige Codierdaten lesen KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet
- [_SAVE_LEAR_EOL_DATA](#job-save-lear-eol-data) - Data available for the LEAR End of Line KWP2000: $3B WriteDataByLocalIdentifier $7B RecordLocalId
- [_READ_LEAR_EOL_DATA](#job-read-lear-eol-data) - KWP 2000: $21   ReadDataByCommonIdentifier KWP 2000: $75   ProjectSpecific
- [_PERFORMANCE_ANALYSIS](#job-performance-analysis) - Reading the Performing Analysis KWP2000: $21 ReadDataByLocalIdentifier $6C RecordLocalId Modus  : Default

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

<a id="job-steuern-memories-loeschen"></a>
### STEUERN_MEMORIES_LOESCHEN

Delete FZM memories (SOLL, IST, secondary, primary) KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-weckringspeicher-loeschen"></a>
### STEUERN_WECKRINGSPEICHER_LOESCHEN

Delete waking registration memory KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE8 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-weckringspeicher-lesen"></a>
### STATUS_WECKRINGSPEICHER_LESEN

Reads waking registration memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE9 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RECORD | string | Register Index |
| STAT_ZEITSTEMPEL | string | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_KILOMETER | string | [Km] |
| STAT_ADDRESS | string | Adresse des Steuergerätes |
| STAT_WAKENDAT | string | Grund des Aufwachens |
| STAT_KLEMMEN_R | string | Grund des Aufwachens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-primaerspeicher-fzm-lesen"></a>
### STATUS_PRIMAERSPEICHER_FZM_LESEN

Reads primary control memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE6 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RECORD | string | Register Index |
| STAT_FEHLER_ID | string | Fehlerart |
| STAT_ADDRESS | string | Adresse des Steuergerätes |
| STAT_ZEITSTEMPEL | string | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_KILOMETER | string | [Km] |
| STAT_STATUS | string | Stand des Monitors |
| STAT_ZUSATZINFO | string | Zusätzliche Information |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sekundaerspeicher-fzm-lesen"></a>
### STATUS_SEKUNDAERSPEICHER_FZM_LESEN

Read secondary control memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE7 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RECORD | string |  |
| STAT_FEHLER_ID | string | Fehlerart |
| STAT_ADDRESS | string | Adresse des Steuergerätes |
| STAT_ZEITSTEMPEL | string | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_KILOMETER | string | [Km] |
| STAT_STATUS | string | Stand des Monitors |
| STAT_ZUSATZINFO | string | Zusätzliche Information |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sollstand-fzm-lesen"></a>
### STATUS_SOLLSTAND_FZM_LESEN

Reads ISTDATEN memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE5 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RECORD | string | Register Index |
| STAT_ADDRESS | string | Adresse des Steuergerätes |
| STAT_RELATIVZEIT | string | Kombi Relativzeit bei Abspeicherung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-iststand-fzm-lesen"></a>
### STATUS_ISTSTAND_FZM_LESEN

Reads ISTDATEN memory KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE4 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RECORD | string | Register Index |
| STAT_ADDRESS | string | Adresse des Steuergerätes |
| STAT_RELATIVZEIT | string | Kombi Relativzeit bei Abspeicherung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-read-memory-by-address"></a>
### _READ_MEMORY_BY_ADDRESS

Selected MEMORY reading by Address KWP 2000: $23  ReadMemoryByAddress KWP 2000: $02  External EEPROM KWP 2000: $04  Internal RAM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Type of Memory to read out 2-&gt;External EEPROM 4-&gt;Internal RAM |
| MEMORY_ADDRESS | long | Address Offset to start reading out Maximum 3 bytes Base Address: e2prom   -&gt;0x00 Ram(ST30)-&gt;0xA0000000 |
| MEMORY_SIZE | int | Number of bytes to be read Max: DiagBufferDataLength-1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-memory-by-address"></a>
### _WRITE_MEMORY_BY_ADDRESS

Selected MEMORY writing by Address KWP 2000: $3D  WriteMemoryByAddress KWP 2000: $02  External EEPROM KWP 2000: $04  Internal RAM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINARY_BUFFER | binary | Binary Buffer Alle Daten in HEX Byte 0	: High Byte Memory Address to write in Byte 1	: Middle Byte Memory Address to write in Byte 2	: Low Byte Memory Address to write in Byte 3	: Type of Memory 2-&gt;External EEPROM 4-&gt;Internal RAM Byte 4	: Number of Data to record Byte 5+ N of Data: Record Values Max. BINARY_BUFFER Size -&gt; DiagBufferDataLength |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-disp-ee"></a>
### _READ_DISP_EE

Read EEPROM EE Struct and Disp Flags KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C000 commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | int | 0-&gt;default 1-&gt;DISP1_ADR,DISP2_ADR 2-&gt;UIF_EEPROM.Aktuelles UserInfoField 3-&gt;PRGREFB.   ProgrammReferenz Backup 4-&gt;VMECUHNB.  VehicleManufacturerECUHardware*Number Backup 5-&gt;PROGS.     Programmierstatus 6-&gt;RANDOM.    Initialisierung des Rauschgenerators |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-disp-ee"></a>
### _WRITE_DISP_EE

Write EEPROM EE Struct and Disp Flags KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFFF commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | int | 0-&gt;default 1-&gt;DISP1_ADR 2-&gt;DISP2_ADR 3-&gt;PROGS |
| WERT | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-brif"></a>
### _READ_BRIF

Lear specific Job for reading BRIF from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C001 commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | int | 0-&gt; default 1-&gt; HWREF.    HardwareReferenz 2-&gt; PECUHN.   physicalECUHardwareNumber 3-&gt; DOECUM.   DateOfECUManufacturing 4-&gt; SSI.      SystemSupplierIndex 5-&gt; SSECUSN.  SystemSupplierECUSerialNumber 6-&gt; ERT.      eraseTime 7-&gt; SIGT.     signTime 8-&gt; RST.      resetTime 9-&gt; MXBL.     maximaleBlockLaenge 10-&gt;VMECUHVN. VehicleManufacturerECUHWVersionNumber 11-&gt;UIF.      UserInfoField Ersteintrag |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-zif"></a>
### _READ_ZIF

Lear specific Job for reading ZIF from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C002 commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | int | 0-&gt;default 1-&gt;PRGREF.    ProgrammReferenz 2-&gt;VMECUHN.   VehicleManufacturerECUHardware*Number 3-&gt;VMECUSLVN. VehicleManufacturerECUSoftwareLayerVersionNumber 4-&gt;VMCI.      VehicleManufacturerCodingIndex 5-&gt;VMDI.      VehicleManufacturerDiagnosticIndex 6-&gt;TO_FILL.   damit signatur bei 0x10050 liegt 7-&gt;SIGNATUR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-length-diag-buffer"></a>
### _READ_LENGTH_DIAG_BUFFER

Read Diag Buffer Lenth KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C003 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_BUFFER_LENGTH | int | Diag Buffer Data Length |
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
| STAT_VERSION_GATEWAY_TABELLE | string | Versionsnummer (Gateway-Tabelle) Result in HEX |
| STAT_VERSION_GATEWAY_SOFTWARE | string | Versionsnummer (Gateway-Software) Result in DEC |
| STAT_VERSION_APPL_SOFTWARE | string | Versionsnummer (Application-Software) Result in DEC |
| STAT_VERSION_OS_SOFTWARE | string | Versionsnummer (Operating System) Result in DEC |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-version-gateway-files"></a>
### _STATUS_VERSION_GATEWAY_FILES

Lesen der Versionsnummer der Gateway software Dateien KWP2000: $21 ReadDataByLocalIdentifier $6A RecordLocalId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSION_GWMAIN_C | int | Versionsnummer der Datei GwMain.c Result in HEX |
| STAT_VERSION_GWMAIN_H | int | Versionsnummer der Datei GwMain.h Result in HEX |
| STAT_VERSION_GWMSGOBJ_C | int | Versionsnummer der Datei GwMsgObj.c Result in HEX |
| STAT_VERSION_GWMSGOBJ_H | int | Versionsnummer der Datei GwMsgObj.h Result in HEX |
| STAT_VERSION_SENDQUEUE_C | int | Versionsnummer der Datei SendQueue.c Result in HEX |
| STAT_VERSION_SENDQUEUE_H | int | Versionsnummer der Datei SendQueue.h Result in HEX |
| STAT_VERSION_LISTUTILS_C | int | Versionsnummer der Datei ListUtils.c Result in HEX |
| STAT_VERSION_LISTUTILS_H | int | Versionsnummer der Datei ListUtils.h Result in HEX |
| STAT_VERSION_GWTABELLE_C | int | Versionsnummer der Datei GwTabelle.c Result in HEX |
| STAT_VERSION_GWTABELLE_H | int | Versionsnummer der Datei GwTabelle.h Result in HEX |
| STAT_VERSION_TYPEDEF_H | int | Versionsnummer der Datei Typedef.h Result in HEX |
| STAT_VERSION_DEBUG_C | int | Versionsnummer der Datei Debug.c Result in HEX |
| STAT_VERSION_DEBUG_H | int | Versionsnummer der Datei Debug.h Result in HEX |
| STAT_VERSION_PERF_C | int | Versionsnummer der Datei Perf.c Result in HEX |
| STAT_VERSION_PERF_H | int | Versionsnummer der Datei Perf.h Result in HEX |
| STAT_VERSION_VERSIONS_C | int | Versionsnummer der Datei Versions.c Result in HEX |
| STAT_VERSION_VERSIONS_H | int | Versionsnummer der Datei Versions.h Result in HEX |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-denormieren"></a>
### STEUERN_FENSTERHEBER_DENORMIEREN

Denormiert gewählten Fensterheber Denormalize selected Window KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $00 FH denormieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER ARGUMENT BESCHREIBUNG) Window Selection Auswahl des Fensterhebers, der denormiert werden soll: 0x13: Fahrerseite hinten 0x14: Beifahrerseite hinten 0x22: Fahrerseite und Beifahrerseite hinten 0x40: Alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-einlernen-ohne-eks"></a>
### STEUERN_FENSTERHEBER_EINLERNEN_OHNE_EKS

Normiert gewählten Fensterheber (ohne EKS) Normalize selected Window (without Apinch) Dauer max. 5 sec KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $01 Einlernen der Fensterheber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER ARGUMENT BESCHREIBUNG) Window Selection Auswahl des Fensters, dass eingelernt werden soll: 0x00: Vorgang abbrechen 0x13: Fahrerseite hinten 0x14: Beifahrerseite hinten 0x22: Fahrerseite und Beifahrerseite hinten 0x40: Alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-einlernen"></a>
### STEUERN_FENSTERHEBER_EINLERNEN

Einlernen der Fensterheber Normiert gewaehlten Fensterheber (mit EKS) Normalize selected Window (with Apinch) Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen Ob Einlernvorgang noch laeuft ist ueber: Job: STATUS_TUER Result: STAT_FH_*_EINLERNENVORGANG_AKTIV abrufbar. Ob ein Fenster eingelernt ist ueber: Result: STAT_FH_*_EINGELERNT KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH EKS JOBS $07 ShortTermAdjustment $02 Hublaenge zum Einlernen aus Codierdaten lesen und Einlernen starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER ARGUMENT BESCHREIBUNG) 0x13: Fahrerseite hinten 0x14: Beifahrerseite hinten 0x22: Fahrerseite und Beifahrerseite hinten 0x40: Alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_VORGANG_GESTARTET_EIN | int | 0: Einlernvorgang konnte nicht gestartet werden 1: Einlernvorgang gestartet |
| STATUS_VORGANG_GESTARTET_DEZIMAL | int | Zuordnung siehe CODE aus table FH_EINLERNEN  CODE BESCHREIBUNG siehe STATUS_VORGANG_GESTARTET_TEXT |
| STATUS_VORGANG_GESTARTET_TEXT | string | Zuordnung siehe BESCHREIBUNG aus table FH_EINLERNEN  CODE BESCHREIBUNG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fensterheber-hinten"></a>
### STATUS_FENSTERHEBER_HINTEN

Gibt aktuellen Zustand Fensterheber wieder Status Rear Windows (z.B. Position, Normierung, Verfahrrichtung, etc) KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $03 Stati der Fensterheber fuer JBBFE2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EKS_HERSTELLER | string | EKS Hersteller 1: BROSE EKS  (Antipinch) 2: KOSTAL EKS (Antipinch) 3: LEAR WCS (No Antipinch. Current Sense blocking) |
| STAT_EKS_SOFTWARE_VERSION | string | EKS Versionsnummer I.XYZ |
| STAT_FH_FAH_OFFEN_KOMPLETT | int | Fenster Fahrerseite hinten komplett offen 0: geschlossen oder halb offen 1: komplett offen |
| STAT_FH_BFH_OFFEN_KOMPLETT | int | Fenster Beifahrerseite hinten komplett offen 0: geschlossen oder halb offen 1: komplett offen |
| STAT_FH_FAH_GESCHLOSSEN | int | Fenster Fahrerseite hinten komplett geschlossen 0: offen oder halb geschlossen 1: komplett geschlossen |
| STAT_FH_BFH_GESCHLOSSEN | int | Fenster Beifahrerseite hinten komplett geschlossen 0: offen oder halb geschlossen 1: komplett geschlossen |
| STAT_FH_FAH_FAEHRT | int | 0: - 1: Fensterheber Fahrerseite hinten faehrt |
| STAT_FH_FAH_FAEHRT_AUF | int | 0: - 1: Fensterheber Fahrerseite hinten faehrt auf |
| STAT_FH_FAH_FAEHRT_ZU | int | 0: - 1: Fensterheber Fahrerseite hinten faehrt zu |
| STAT_FH_BFH_FAEHRT | int | 0: - 1: Fensterheber Beifahrerseite hinten faehrt |
| STAT_FH_BFH_FAEHRT_AUF | int | 0: - 1: Fensterheber Beifahrerseite hinten faehrt auf |
| STAT_FH_BFH_FAEHRT_ZU | int | 0: - 1: Fensterheber Beifahrerseite hinten faehrt zu |
| STAT_FH_FAH_EINGELERNT | int | 0: Fensterheber Fahrerseite hinten nicht eingelernt 1: Fensterheber Fahrerseite hinten eingelernt |
| STAT_FH_BFH_EINGELERNT | int | 0: Fensterheber Beifahrerseite hinten nicht eingelernt 1: Fensterheber Beifahrerseite hinten eingelernt |
| STAT_FH_FAH_INITRESULT | int | Status des letzten/aktuellen Initlaufes des Fensterheber Fahrerseite hinten Zuordnung siehe BESCHREIBUNG aus table FH_EINLERNEN  CODE BESCHREIBUNG 0: NO INIT STARTED, 1: INIT RUNNING, 2: INIT COMPLETED 3: ERROR BUSY, 4: ERROR USER STOP, 5: ERROR REVERSE, 6: ERROR INIT |
| STAT_FH_FAH_INITRESULT_TEXT | string | Wert im Text der Variable STAT_FH_FAH_INITRESULT |
| STAT_FH_BFH_INITRESULT | int | Status des letzten/aktuellen Initlaufes des Fensterheber Beifahrerseite hinten Zuordnung siehe BESCHREIBUNG aus table FH_EINLERNEN  CODE BESCHREIBUNG 0: NO INIT STARTED, 1: Initialisierung laeuft, 2: Initialisierung abgeschlossen 3: FEHLER: Busy, 4: FEHLER: Abbruch durch Anwender, 5: FEHLER: Reversierer, 6: FEHLER: Init |
| STAT_FH_BFH_INITRESULT_TEXT | string | Wert im Text der Variable STAT_FH_BFH_INITRESULT |
| STAT_FH_FAH_POSITION_WERT | int | Position Fensterheber Fahrerseite hinten im Pulses (1/4 Motorumdrehungen) nur bei eingelerntem FH Wertbereich: PL4:     0-1150 pulses PL2-RED: 0-1710 pulses |
| STAT_FH_FAH_POSITION_EINH | string | Einheit Position Fensterheber Fahrerseite hinten Puls |
| STAT_FH_FAH_POSITION_MM_WERT | int | Position Fensterheber Fahrerseite hinten im Millimeter, nur bei eingelerntem FH Wertbereich: PL4:     0-550 mm PL2-RED: 0-450 mm |
| STAT_FH_FAH_POSITION_MM_EINH | string | Einheit Position Fensterheber Fahrerseite hinten Mm |
| STAT_FH_BFH_POSITION_WERT | int | Position Fensterheber Beifahrerseite hinten im Pulses (1/4 Motorumdrehungen) nur bei eingelerntem FH Wertbereich: PL4:     0-1150 pulses PL2-RED: 0-1710 pulses |
| STAT_FH_BFH_POSITION_EINH | string | Einheit Position Fensterheber Beifahrerseite hinten Puls |
| STAT_FH_BFH_POSITION_MM_WERT | int | Position Fensterheber Beifahrerseite hinten im Millimeter, nur bei eingelerntem FH Wertbereich: PL4:     0-550 mm PL2-RED: 0-450 mm |
| STAT_FH_BFH_POSITION_MM_EINH | string | Einheit Position Fensterheber Beifahrerseite hinten Mm |
| STAT_FH_FAH_CUT_OUT | int | 0: - 1: Fensterheber Fahrerseite hinten Reversierung |
| STAT_FH_BFH_CUT_OUT | int | 0: - 1: Fensterheber Beifahrerseite hinten Reversierung |
| STAT_FH_FAH_OVERHEAT_90 | int | 0: - 1: Fensterheber Fahrerseite hinten Temperatur ueber 90°C |
| STAT_FH_BFH_OVERHEAT_90 | int | 0: - 1: Fensterheber Beifahrerseite hinten Temperatur ueber 90°C |
| STAT_FH_FAH_OVERHEAT_100 | int | 0: - 1: Fensterheber Fahrerseite hinten Temperatur ueber 100°C |
| STAT_FH_BFH_OVERHEAT_100 | int | 0: - 1: Fensterheber Beifahrerseite hinten Temperatur ueber 100°C |
| STAT_FH_FAH_HALL_DEFEKT | int | 0: - 1: Fensterheber Fahrerseite hinten Hall Defekt entweder Hall 1 oder Hall 2 |
| STAT_FH_BFH_HALL_DEFEKT | int | 0: - 1: Fensterheber Beifahrerseite hinten Hall Defekt entweder Hall 1 oder Hall 2 |
| STAT_FH_FAH_RELAIS_1_DEFEKT | int | 0: - 1: Fensterheber Fahrerseite hinten Relais 1 ZU Defekt |
| STAT_FH_BFH_RELAIS_1_DEFEKT | int | 0: - 1: Fensterheber Beifahrerseite hinten Relais 1 ZU Defekt |
| STAT_FH_FAH_RELAIS_2_DEFEKT | int | 0: - 1: Fensterheber Fahrerseite hinten Relais 2 AUF Defekt |
| STAT_FH_BFH_RELAIS_2_DEFEKT | int | 0: - 1: Fensterheber Beifahrerseite hinten Relais 2 AUF Defekt |
| STAT_FH_FAH_EE_CHECKSUM_ERROR | int | 0: - 1: Fensterheber Fahrerseite hinten E² Spiegel Checksummen Fehler |
| STAT_FH_BFH_EE_CHECKSUM_ERROR | int | 0: - 1: Fensterheber Beifahrerseite hinten E² Spiegel Checksummen Fehler |
| STAT_FH_FAH_STROKELENGTH | int | 0: - 1: Fensterheber Fahrerseite hinten Hublaenge In 1/4 Motorumdrehungen (Pulses) |
| STAT_FH_BFH_STROKELENGTH | int | 0: - 1: Fensterheber Beifahrerseite hinten Hublaenge In 1/4 Motorumdrehungen (Pulses) |
| STAT_FH_FAH_DRIVE_COUNT_AFTER_INIT | int | 0: - 1: Fensterheber Fahrerseite hinten Anzahl Heben Ansteuerungen nach Init/Denormieren Wertbereich: 0...0xFFFF |
| STAT_FH_BFH_DRIVE_COUNT_AFTER_INIT | int | 0: - 1: Fensterheber Beifahrerseite hinten Anzahl Heben Ansteuerungen nach Init/Denormieren Wertbereich: 0...0xFFFF |
| STAT_FH_FAH_STROKE_TIME | int | 0: - 1: Fensterheber Fahrerseite hinten Zeit fuer Initialisierungslauf heben In 10 ms |
| STAT_FH_BFH_STROKE_TIME | int | 0: - 1: Fensterheber Beifahrerseite hinten Zeit fuer Initialisierungslauf heben In 10 ms |
| STAT_FH_FAH_DRIVE_ACK | int | Fensterheber Fahrerseite hinten 0: out_drive ungueltig 1: out_drive gueltig |
| STAT_FH_BFH_DRIVE_ACK | int | Fensterheber Beifahrerseite hinten 0: out_drive ungueltig 1: out_drive gueltig |
| STAT_FH_FAH_NOT_READY_FOR_SLEEP | int | Fensterheber Fahrerseite hinten 0: - 1: Fensterheber EKS SW nicht bereit um schlafen zu gehen |
| STAT_FH_BFH_NOT_READY_FOR_SLEEP | int | Fensterheber Beifahrerseite hinten 0: - 1: Fensterheber EKS SW nicht bereit um schlafen zu gehen |
| STAT_FH_FAH_ENABLE_EKS | int | Fensterheber Fahrerseite hinten 0: - 1: EKS aktivieren |
| STAT_FH_BFH_ENABLE_EKS | int | Fensterheber Beifahrerseite hinten 0: - 1: EKS aktivieren |
| STAT_FH_FAH_DOORAJAR | int | Fensterheber Fahrerseite hinten 0: Tuerkontakt geschlossen 1: Tuerkontakt offen |
| STAT_FH_BFH_DOORAJAR | int | Fensterheber Beifahrerseite hinten 0: Tuerkontakt geschlossen 1: Tuerkontakt offen |
| STAT_FH_FAH_PANIC_ONE | int | Fensterheber Fahrerseite hinten 0: - 1: Panikmodus |
| STAT_FH_BFH_PANIC_ONE | int | Fensterheber Beifahrerseite hinten 0: - 1: Panikmodus |
| STAT_FH_FAH_INITJOB | int | Fensterheber Fahrerseite hinten 0: - 1: Einlernjob |
| STAT_FH_BFH_INITJOB | int | Fensterheber Beifahrerseite hinten 0: - 1: Einlernjob |
| STAT_FH_FAH_LOCKSTATE | int | Fensterheber Fahrerseite hinten 0: unverschlossen 1: zugeschlossen |
| STAT_FH_BFH_LOCKSTATE | int | Fensterheber Beifahrerseite hinten 0: unverschlossen 1: zugeschlossen |
| STAT_FH_FAH_OTHER_WINDOW_STATE | int | Fensterheber Fahrerseite hinten 0: offen 1: geschlossen |
| STAT_FH_BFH_OTHER_WINDOW_STATE | int | Fensterheber Beifahrerseite hinten 0: offen 1: geschlossen |
| STAT_FH_FAH_MOTOR_P | int | Fensterheber Fahrerseite hinten Zustand der Motorleitung+ 0: low 1: high |
| STAT_FH_FAH_MOTOR_M | int | Fensterheber Fahrerseite hinten Zustand der Motorleitung- 0: low 1: high |
| STAT_FH_BFH_MOTOR_P | int | Fensterheber Beifahrerseite hinten Zustand der Motorleitung+ 0: low 1: high |
| STAT_FH_BFH_MOTOR_M | int | Fensterheber Beifahrerseite hinten Zustand der Motorleitung- 0: low 1: high |
| STAT_FH_USASTANDART | int | USA Reversierweg 0: alle anderen 1: fur USA, Kanada, Korea |
| STAT_KL_15 | int | 0: KL 15 OFF 1: KL 15 ON |
| STAT_KL_50 | int | 0: KL 50 OFF 1: KL 50 ON |
| STAT_FETRAWE | int | 0: AUS 1: Fertigung 2: Transport 4: Werkstatt |
| STAT_FH_ENABLE | int | Fensterheber Freischaltung Aus K-CAN Nachricht 0x26E 0: deaktiviert 1: aktiviert |
| STAT_FH_PANICMODE | int | Fensterheber Panikmodus Aus K-CAN Nachricht 0x26E 0: deaktiviert 1: aktiviert |
| STAT_KINDERSICHERUNG | int | Fensterheber Kindersicherung Aus K-CAN Nachricht 0x26E 0: deaktiviert, Local Tasters Enable 1: aktiviert, Local Tasters Diseable |
| STAT_GESCHWINDIGKEIT_FAHRZEUG_WERT | unsigned int | Fahrzeug Geschwindigkeit Aus PT-CAN Nachricht 0x1A0 Wertebereich: 0..0xFF (HEX)&lt;-&gt;0..255 [km/h] |
| STAT_GESCHWINDIGKEIT_FAHRZEUG_EINH | string | Einheit fuer Fahrzeug Geschwindigkeit: [km/h] |
| STAT_AUSSENTEMPERATUR_WERT | int | Aussentemperatur Aus K-CAN Nachricht 0x2CA Wertebereich: 0..0xFF (HEX)&lt;-&gt;0..255 |
| STAT_AUSSENTEMPERATUR_TEXT | real | Interpretation Aussentemperatur Aus K-CAN Nachricht 0x2CA (T)= 0,5 * (HEX)-40 [°C], -40..+85 [°C] |
| STAT_AUSSENTEMPERATUR_EINH | string | Einheit fuer Aussentemperatur: [°C] |
| STAT_RELATIVZEIT_WERT | unsigned long | Relativzeit Aus K-CAN Nachricht 0x328 Wertebereich:0..0xFFFFFFFF&lt;-&gt;0..4.294.967.294 [sek] (136,9 jahres) |
| STAT_RELATIVZEIT_EINH | string | Einheit fuer Relativzeit: [sek] |
| STAT_FH_FAH_MOTOR_VOLTAGE_WERT | int | Fensterheber Fahrerseite hinten Motor Spannung Wertebereich: 0..0xFF (HEX)&lt;-&gt;0..255 [°C] Aufloesung 0,074 V/Bit |
| STAT_FH_FAH_MOTOR_VOLTAGE_TEXT | real | Fensterheber Fahrerseite hinten Interpretation Motor Spannung Aufloesung 0,074 V/Bit Wertbereich: 0..18,87 [V] Vm=(HEX)*0.074 [V], for Vref=5V |
| STAT_FH_FAH_MOTOR_VOLTAGE_EINH | string | Einheit fuer Motor Spannung: [Volt] |
| STAT_FH_BFH_MOTOR_VOLTAGE_WERT | int | Fensterheber Beifahrerseite hinten Motor Spannung Wertebereich: 0..0xFF (HEX)&lt;-&gt;0..255 Aufloesung 0,074 V/Bit |
| STAT_FH_BFH_MOTOR_VOLTAGE_TEXT | real | Fensterheber Beifahrerseite hinten Interpretation Motor Spannung Aufloesung 0,074 V/Bit Wertbereich: 0..18,87 [V] Vm=(HEX)*0.074 [V], for Vref=5V |
| STAT_FH_BFH_MOTOR_VOLTAGE_EINH | string | Einheit fuer Motor Spannung: [Volt] |
| STAT_UBATT_LOW | int | 0: Keine Unterspannung detektiert 1: Unterspannung (&lt;12V) an Klemme 30 detektiert (min. Spannung für das Einlernen der Fenster) |
| STAT_UBATT_OVR | int | 0: Keine Ueberspannung detektiert 1: Ueberspannung (&gt;16V) an Klemme 30 detektiert |
| STAT_UBATT_WERT | int | Batterie Spannung (Klemme 30) Wertbereich: 0..0x3FF (1023) Aufloesung 0,0277 V/Bit |
| STAT_UBATT_TEXT | real | Interpretation Batterie Spannung Aufloesung 0,028 V/Bit Wertbereich: 0..28,40 [V] Vbat=(HEX)*0,028 [V], for Vref=5V |
| STAT_UBATT_EINH | string | Einheit fuer Batterie Spannung: [Volt] |
| STAT_FH_TASTERFAH_FAH_WERT | int | Fahrerseite hinten (lokaler Taster) Fensterheber Fahrerseite hinten 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) |
| STAT_FH_TASTERFAH_FAH_TEXT | string | Fahrerseite hinten (lokaler Taster) Fensterheber Fahrerseite hinten Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 |
| STAT_FH_TASTERBFH_BFH_WERT | int | Beifahrerseite hinten (lokaler Taster) Fensterheber Beifahrerseite hinten 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) |
| STAT_FH_TASTERBFH_BFH_TEXT | string | Beifahrerseite hinten (lokaler Taster) Fensterheber Beifahrerseite hinten Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 |
| STAT_FH_TASTERFA_FAH_WERT | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite hinten Aus K-CAN Nachricht 0xFA 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) |
| STAT_FH_TASTERFA_FAH_TEXT | string | Fahrerseite (Tastenblock) Fensterheber Fahrerseite hinten Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 |
| STAT_FH_TASTERFA_BFH_WERT | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten Aus K-CAN Nachricht 0xFA 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) |
| STAT_FH_TASTERFA_BFH_TEXT | string | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 |
| STAT_FH_KOMFORT_FAH_WERT | int | Fahrerseite (Komfortfunktion) Fensterheber Fahrerseite hinten Aus K-CAN Nachricht 0x26E 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) |
| STAT_FH_KOMFORT_FAH_TEXT | string | Fahrerseite (Komfortfunktion) Fensterheber Fahrerseite hinten Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 |
| STAT_FH_KOMFORT_BFH_WERT | int | Fahrerseite (Komfortfunktion) Fensterheber Beifahrerseite hinten Aus K-CAN Nachricht 0x26E 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) |
| STAT_FH_KOMFORT_BFH_TEXT | string | Fahrerseite (Komfortfunktion) Fensterheber Beifahrerseite hinten Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 |
| STAT_FH_TASTERBF_BF_WERT | int | Beifahrerseite (lokaler Taster) Fensterheber Beifahrerseite 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) |
| STAT_FH_TASTERBF_BF_TEXT | string | Beifahrerseite (lokaler Taster) Fensterheber Beifahrerseite Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-hinten"></a>
### STEUERN_FENSTERHEBER_HINTEN

Verfaehrt gewaehlten Fensterheber gemaeß Control Rear Windows angegebener Richtung und Zeit (ms) KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $04 Ansteuern FH

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG_FH_FAH | string | table FH_RICHTUNG AUSWAHL_RICHTUNG TEXT Driving direction Rear Driver Window Auswahl der Richtung, in der das Fahrertuerfenster verfahren soll: AUS(0), AUF(1), ZU(2) |
| ANSTEUER_ZEIT_FAH | int | Driving Time Rear Driver Door, in steps of 100 ms Zeit in 100ms, die der FH angesteuert werden soll, d.h. 1 = 100ms 15 sek. max. (150) 0: kein FATH Steuern |
| RICHTUNG_FH_BFH | string | table FH_RICHTUNG AUSWAHL_RICHTUNG TEXT Driving direction Rear Passenger Window Auswahl der Richtung, in der das Beiahrertuerfenster verfahren soll: AUS(0), AUF(1), ZU(2) |
| ANSTEUER_ZEIT_BFH | int | Driving Time Rear Driver Door, in steps of 100 ms Zeit in 100ms, die der FH angesteuert werden soll, d.h. 1 = 100ms 15 sek. max. (150) 0: kein BFTH Steuern |
| IM_PANIK_MODUS | int | Control Window in Panic Mode Step 1 Ansteuern den FH im Panikmodus Stufe 1 NORMAL MODUS(0), PANIK MODUS(1) default: NORMAL MODUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-denormierer"></a>
### STATUS_FH_LOGGER_DENORMIERER

Fensterheber Denormierungslogger auslesen Lesen von EE_FH_LOG_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $05 EE_FH_LOG_DATA Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EE_FH_LOG_DATA | binary | ausgelesene Daten von EE_FH_LOG_DATA |
| STAT_DENORMIERUNGS_COUNTER | unsigned int | Daten von SG Denormierungscounter bis 65535, danach wird nur noch auf Datensatznummer '5' gespeichert |
| STAT_DATENSATZ_1 | string | Datensatznummer letzter abgespeicherter Datensatz |
| STAT_FEHLERNUMMER_1 | int | Fehlernummer des Denormierers |
| STAT_FEHLERNUMMER_TEXT_1 | string | Fehlertext des Denormierers |
| STAT_HEADER_1 | int | Detailinformation zum Fehler |
| STAT_HEADER_TEXT_1 | string | Text zur Detailinformation |
| STAT_POSITION_HZ_1 | int | Scheibenposition in Hallimpulsen |
| STAT_VOLTAGE_WERT_1 | int | Spannung am Fensterheber in Volt |
| STAT_FEHLERFLAGS_1 | int | Fehlerdigitalstati Block 1 |
| STAT_FEHLERFLAGS_TEXT_1 | string | Fehlerstati Block 1 als Text |
| STAT_HALLFLAGS_1 | int | Fehlerdigitalstati Block 2 |
| STAT_HALLFLAGS_TEXT_1 | string | Fehlerstati Block 2 als Text |
| STAT_DATENSATZ_2 | string | Datensatznummer vorletzter abgespeicherter Datensatz |
| STAT_FEHLERNUMMER_2 | int | Fehlernummer des Denormierers |
| STAT_FEHLERNUMMER_TEXT_2 | string | Fehlertext des Denormierers |
| STAT_HEADER_2 | int | Detailinformation zum Fehler |
| STAT_HEADER_TEXT_2 | string | Text zur Detailinformation |
| STAT_POSITION_HZ_2 | int | Scheibenposition in Hallimpulsen |
| STAT_VOLTAGE_WERT_2 | int | Spannung am Fensterheber in Volt |
| STAT_FEHLERFLAGS_2 | int | Fehlerdigitalstati Block 1 |
| STAT_FEHLERFLAGS_TEXT_2 | string | Fehlerstati Block 1 als Text |
| STAT_HALLFLAGS_2 | int | Fehlerdigitalstati Block 2 |
| STAT_HALLFLAGS_TEXT_2 | string | Fehlerstati Block 2 als Text |
| STAT_DATENSATZ_3 | string | Datensatznummer drittletzter abgespeicherter Datensatz |
| STAT_FEHLERNUMMER_3 | int | Fehlernummer des Denormierers |
| STAT_FEHLERNUMMER_TEXT_3 | string | Fehlertext des Denormierers |
| STAT_HEADER_3 | int | Detailinformation zum Fehler |
| STAT_HEADER_TEXT_3 | string | Text zur Detailinformation |
| STAT_POSITION_HZ_3 | int | Scheibenposition in Hallimpulsen |
| STAT_VOLTAGE_WERT_3 | int | Spannung am Fensterheber in Volt |
| STAT_FEHLERFLAGS_3 | int | Fehlerdigitalstati Block 1 |
| STAT_FEHLERFLAGS_TEXT_3 | string | Fehlerstati Block 1 als Text |
| STAT_HALLFLAGS_3 | int | Fehlerdigitalstati Block 2 |
| STAT_HALLFLAGS_TEXT_3 | string | Fehlerstati Block 2 als Text |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-denormierer-lear"></a>
### _STATUS_FH_LOGGER_DENORMIERER_LEAR

Fensterheber Denormierungslogger auslesen Lesen von EE_FH_LOG_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $05 EE_FH_LOG_DATA Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EE_FH_LOG_DATA | binary | ausgelesene Daten von EE_FH_LOG_DATA |
| STAT_DENORMIERUNGS_COUNTER | unsigned int | Daten von SG Denormierungscounter bis 65535, danach wird nur noch auf Datensatznummer '5' gespeichert |
| STAT_DATENSATZ | string | Datensatznummer |
| STAT_FEHLERNUMMER | int | Fehlernummer des Denormierers |
| STAT_FEHLERNUMMER_TEXT | string | Fehlertext des Denormierers |
| STAT_HEADER | int | Detailinformation zum Fehler |
| STAT_HEADER_TEXT | string | Text zur Detailinformation |
| STAT_POSITION_HZ | int | Scheibenposition in Hallimpulsen |
| STAT_VOLTAGE_WERT | int | Spannung am Fensterheber in Volt |
| STAT_FEHLERFLAGS | int | Fehlerdigitalstati Block 1 |
| STAT_FEHLERFLAGS_TEXT | string | Fehlerstati Block 1 als Text |
| STAT_HALLFLAGS | int | Fehlerdigitalstati Block 2 |
| STAT_HALLFLAGS_TEXT | string | Fehlerstati Block 2 als Text |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fh-logger-denormierer"></a>
### STEUERN_FH_LOGGER_DENORMIERER

Denormierungslogger löschen Loeschen von EE_FH_LOG_DATA des jbbfe2 KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $05 EE_FH_LOG_DATA Loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-reversierer"></a>
### STATUS_FH_LOGGER_REVERSIERER

Fensterheber Reversierlogger auslesen Lesen von EE_FH_REV_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $08 EE_FH_REV_DATA Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EE_FH_REV_DATA | binary | ausgelesene Daten von EE_FH_REV_DATA |
| STAT_REVERSIERUNGS_COUNTER | unsigned int | absolute Zahl der Reversierer, 0 - 65535 |
| STAT_DATENSATZ_1 | string | Nummer des letzten Datensatzes |
| STAT_FEHLERNUMMER_1 | int | Fehlernummer des letzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_1 | string | Fehlertext des letzten Reversierers |
| STAT_POSITION_HZ_1 | int | Scheibenposition in Hallsignale beim letzten Reversierer |
| STAT_VOLTAGE_WERT_1 | real | Fensterheberspannung beim letzten Reversierer |
| STAT_AUSSENTEMP_WERT_1 | real | Aussentemperatur in °C beim letzten Reversierer |
| STAT_SPEED_WERT_1 | real | Fahrzeuggeschwindigkeit in km/h beim letzten Reversierer |
| STAT_DATENSATZ_2 | string | Nummer des vorletzten Datensatzes |
| STAT_FEHLERNUMMER_2 | int | Fehlernummer des vorletzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_2 | string | Fehlertext des vorletzten Reversierers |
| STAT_POSITION_HZ_2 | int | Scheibenposition in Hallsignale beim vorletzten Reversierer |
| STAT_VOLTAGE_WERT_2 | real | Fensterheberspannung beim vorletzten Reversierer |
| STAT_AUSSENTEMP_WERT_2 | real | Aussentemperatur in °C beim vorletzten Reversierer |
| STAT_SPEED_WERT_2 | real | Fahrzeuggeschwindigkeit in km/h beim vorletzten Reversierer |
| STAT_DATENSATZ_3 | string | Nummer des drittletzten Datensatzes |
| STAT_FEHLERNUMMER_3 | int | Fehlernummer des drittletzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_3 | string | Fehlertext des drittletzten Reversierers |
| STAT_POSITION_HZ_3 | int | Scheibenposition in Hallsignale beim drittletzten Reversierer |
| STAT_VOLTAGE_WERT_3 | real | Fensterheberspannung beim drittletzten Reversierer |
| STAT_AUSSENTEMP_WERT_3 | real | Aussentemperatur in °C beim drittletzten Reversierer |
| STAT_SPEED_WERT_3 | real | Fahrzeuggeschwindigkeit in km/h beim drittletzten Reversierer |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-reversierer-lear"></a>
### _STATUS_FH_LOGGER_REVERSIERER_LEAR

Fensterheber Reversierlogger auslesen Lesen von EE_FH_REV_DATA KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $08 EE_FH_REV_DATA Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EE_FH_REV_DATA | binary | ausgelesene Daten von EE_FH_REV_DATA |
| STAT_REVERSIERUNGS_COUNTER | unsigned int | absolute Zahl der Reversierer, 0 - 65535 |
| STAT_DATENSATZ | string | Datensatz Nummer |
| STAT_FEHLERNUMMER | int | Fehlernummer des Reversierers |
| STAT_FEHLERNUMMER_TEXT | string | Fehlertext des Reversierers |
| STAT_POSITION_HZ | int | Scheibenposition in Hallsignale |
| STAT_VOLTAGE_WERT | real | Fensterheberspannung |
| STAT_AUSSENTEMP_WERT | real | Aussentemperatur in °C |
| STAT_SPEED_WERT | real | Fahrzeuggeschwindigkeit in km/h |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fh-logger-reversierer"></a>
### STEUERN_FH_LOGGER_REVERSIERER

Reversierungslogger löschen Loeschen von EE_FH_REV_DATA des jbbfe2 KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH BROSE JOBS $07 ShortTermAdjustment $08 EE_FH_REV_DATA Loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-messdaten-aktivieren"></a>
### STEUERN_FENSTERHEBER_MESSDATEN_AKTIVIEREN

Messdatenausgabe fuer FH starten KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $06 MESSDATEN_AKTIVIEREN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER ARGUMENT BESCHREIBUNG) Window Selection 0x00: Vorgang abbrechen 0x13: Fahrerseite hinten 0x14: Beifahrerseite hinten 0x22: Fahrerseite und Beifahrerseite hinten 0x40: Alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-qualitaet-fensterheberlauf"></a>
### STATUS_QUALITAET_FENSTERHEBERLAUF

Qualitaetsbewertung Fensterheber Fensterheber muss eingelernt sein und mind. einmalig mit Panikoption = 1 verfahren worden sein KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $XX XX

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_BAUREIHE | string | Auswahl der Baureihe (ARGUMENT aus table FH_AUSWAHL_BAUREIHE) Default -&gt; E70 E70: E70 E87: E87 E90: E90 E91: E91 E92: E92 E93: E93 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| STAT_AUSWERTUNG_GUELTIG_WERT | int | 1 -&gt; gueltig 0 -&gt; ungueltig |
| STAT_AUSWERTUNG_GUELTIG_TEXT | string | Textuelle Beschreibung, ob Auswertung gueltig |
| STAT_AUSWERTUNG_FAHRER_HINTEN | string | Interpretation Adaptionsdaten Fahrerseite hinten Bei Kategorie 9, 8 und 7 wird die Oeffnungsweite des Fensters an der B-Saeule ausgegeben mit zugehoerigen Adaptionswert |
| STAT_KATEGORIE_FAHRER_HINTEN_WERT | int | Kategorie Fahrerseite hinten als Integer |
| STAT_AUSWERTUNG_BEIFAHRER_HINTEN | string | Interpretation Adaptionsdaten Beifahrerseite hinten Bei Kategorie 9, 8 und 7 wird die Oeffnungsweite des Fensters an der B-Saeule ausgegeben mit zugehoerigen Adaptionswert |
| STAT_KATEGORIE_BEIFAHRER_HINTEN_WERT | int | Kategorie Beifahrerseite hinten als Integer |
| STAT_HUBZEIT_FAHRER_HINTEN | int | Hubzeit Fahrerseite hinten in 10 ms |
| STAT_HUBZEIT_BEIFAHRER_HINTEN | int | Hubzeit Beifaherseite hinten in 10 ms |
| STAT_AUSWERTUNG_HUBZEIT_FAHRER_HINTEN | string | Interpretation Hubzeit Fahrerseite hinten |
| STAT_AUSWERTUNG_HUBZEIT_BEIFAHRER_HINTEN | string | Interpretation Hubzeit Beifahrerseite hinten |
| STAT_ADAPTIONSDATEN_FAHRER_HINTEN | binary | ausgelesene Daten Fahrerseite hinten |
| STAT_ADAPTIONSDATEN_BEIFAHRER_HINTEN | binary | ausgelesene Daten Beifahrerseite hinten |
| STAT_INFO_GRENZWERTE | string | verwendete Grenzwerte |
| STAT_INFO_AUSWAHL_BAUREIHE | int | Auswahl Baureihe |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-adaptionsspeicher-lesen"></a>
### _STATUS_FH_ADAPTIONSSPEICHER_LESEN

Adaptionsdaten Fensterheber KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $07 ECHT_ZEIT_DATEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ADAPTIONSDATEN_FAHRER | binary | ausgelesene Daten Fahrerseite |
| STAT_ADAPTIONSDATEN_BEIFAHRER | binary | ausgelesene Daten Beifahrerseite |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fh-adaptionsspeicher-loeschen"></a>
### STEUERN_FH_ADAPTIONSSPEICHER_LOESCHEN

Adaptionsdaten Fensterheber Loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $0E ECHT_ZEIT_DATEN ZONE 4 Loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-echtzeitdaten-brose-lesen"></a>
### _ECHTZEITDATEN_BROSE_LESEN

Echtzeitdaten vom Brose auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $01 ReportCurrentState $07 ECHT_ZEIT_DATEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_ZONE | int | Auswahl der Zone auszulesen 1 -&gt; zone_4_1_fat [0]..[84] 2 -&gt; zone_4_2_fat [85]..[169] 3 -&gt; zone_4_3_fat [170]..[254] 4 -&gt; zone_4_4_fat [255]..[283] 5 -&gt; zone_5_fat 6 -&gt; zone_6_fat 7 -&gt; zone_7_fat 8 -&gt; zone_4_1_bft [0]..[84] 9 -&gt; zone_4_2_bft [85]..[169] 10 -&gt; zone_4_3_bft [170]..[254] 11 -&gt; zone_4_4_bft [255]..[283] 12 -&gt; zone_5_bft 13 -&gt; zone_6_bft 14 -&gt; zone_7_bft |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZONE_ANZAHL | string | ausgelesene Daten von ECHT_ZEIT_DATEN |
| STAT_ZONE_DATA | binary | ausgelesene Daten von ECHT_ZEIT_DATEN |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnose-brose-fh-1"></a>
### _STEUERN_DIAGNOSE_BROSE_FH_1

Status von JBBFE2 schreiben KWP2000: $30 InputOutputControlByLocalIdentifier $07 FH WOUT Logik JOBS $07 ShortTermAdjustment $09 Diagnose fuer BROSE-FH

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BROSE_DATEN_1 | string | Diagnosedaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-eks-coddata"></a>
### _STATUS_FH_EKS_CODDATA

Coding EKS BROSE reading from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $3500-0x350F commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EKS_AUSWAHL | int | Select EKS(Apinch) Supplier 1: BROSE 2: KOSTAL |
| BLOCK | int | Coding Block to read out: BROSE:  0-15 KOSTAL: 0-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EKS_HERSTELLER | string | EKS(Apinch) Supplier 1: BROSE 2: KOSTAL |
| STAT_COD_DATA | binary | Coding Data read |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fh-eks-coddata"></a>
### _STEUERN_FH_EKS_CODDATA

Coding EKS BROSE writing to EEPROM and RAM KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $3500-0x350F commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINARY_BUFFER | binary | Binary Buffer Alle Daten in HEX EKS Hersteller Auswahl Byte 0	: EKS(Apinch) Supplier (1: BROSE, 2: KOSTAL) Byte 1	: Coding Block to write in (0-15) Byte 2 + 15: Data to record (16 Bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EKS_HERSTELLER | string | EKS(Apinch) Supplier 1: BROSE 2: KOSTAL |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode-funktional"></a>
### _SLEEP_MODE_FUNKTIONAL

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse_LEAR F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |
| OHNE_POWERMODUL | string | Power Down ohne Powermodul Werte: JA, NEIN table DigitalArgument TEXT Defaultwert: NEIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode-lear"></a>
### _SLEEP_MODE_LEAR

Send ECU to Sleep Mode without waiting the busses to stop KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $02 Specific Lear Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-historienspeicher-lesen-block-1"></a>
### STATUS_HISTORIENSPEICHER_LESEN_BLOCK_1

EnergieDatenSpeicher Teil 1 -Einschlafverhinderer- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE1 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DATENSATZ_1 | string | Datens des ersten Einschlafverhinderers |
| STAT_VERURSACHER_1 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_1 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_1 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_1 | string | Einheit fuer KM_STAND: KM |
| STAT_HAUFIGKEIT_1 | int | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_2 | string | Daten des zweiten Einschlafverhinderers |
| STAT_VERURSACHER_2 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_2 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_2 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_2 | string | Einheit fuer KM_STAND: KM |
| STAT_HAUFIGKEIT_2 | int | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_3 | string | Daten des dritten Einschlafverhinderers |
| STAT_VERURSACHER_3 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_3 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_3 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_3 | string | Einheit fuer KM_STAND: KM |
| STAT_HAUFIGKEIT_3 | int | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_4 | string | Daten des vierten Einschlafverhinderers |
| STAT_VERURSACHER_4 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_4 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_4 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_4 | string | Einheit fuer KM_STAND: KM |
| STAT_HAUFIGKEIT_4 | int | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_5 | string | Daten des fünften Einschlafverhinderers |
| STAT_VERURSACHER_5 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_5 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_5 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_5 | string | Einheit fuer KM_STAND: KM |
| STAT_HAUFIGKEIT_5 | int | Einheit fuer KM_STAND: KM |
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
| STAT_DATENSATZ_0 | string | Aktuelle Woche |
| STAT_RELATIVZEIT_BEGINN_WERT_0 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_0 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_0 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_0 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_0 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_0 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_0 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_0 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_0 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_RELATIVZEIT_OFFSET_WERT_0 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_OFFSET_EINH_0 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_SLEEP_WERT_0 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_SLEEP_EINH_0 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KOMBI_RESET_0 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_DATENSATZ_1 | string | Eine Woche vorher |
| STAT_RELATIVZEIT_BEGINN_WERT_1 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_1 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_1 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_1 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_1 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_1 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_1 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_1 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_RELATIVZEIT_OFFSET_WERT_1 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_OFFSET_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_SLEEP_WERT_1 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_SLEEP_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KOMBI_RESET_1 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_DATENSATZ_2 | string | Zwei Wochen vorher |
| STAT_RELATIVZEIT_BEGINN_WERT_2 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_2 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_2 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_2 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_2 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_2 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_2 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_2 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_RELATIVZEIT_OFFSET_WERT_2 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_OFFSET_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_SLEEP_WERT_2 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_SLEEP_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KOMBI_RESET_2 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_DATENSATZ_3 | string | Drei Wochen vorher |
| STAT_RELATIVZEIT_BEGINN_WERT_3 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_3 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_3 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_3 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_3 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_3 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_3 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_3 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_RELATIVZEIT_OFFSET_WERT_3 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_OFFSET_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_SLEEP_WERT_3 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_SLEEP_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KOMBI_RESET_3 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_DATENSATZ_4 | string | Vier Wochen Vorher |
| STAT_RELATIVZEIT_BEGINN_WERT_4 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_4 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_4 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_4 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_4 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_4 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_4 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_4 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_RELATIVZEIT_OFFSET_WERT_4 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_OFFSET_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_SLEEP_WERT_4 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_SLEEP_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KOMBI_RESET_4 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_DATENSATZ_5 | string | Fuenf Woche vorher |
| STAT_RELATIVZEIT_BEGINN_WERT_5 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_5 | unsigned int | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_GESAMTE_KM_EINH_5 | string | Einheit fuer GESAMTE_KM: KM |
| STAT_ANZAHL_FAHRTEN_0_5_KM_5 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_5 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_5 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_5 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_5 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_RELATIVZEIT_OFFSET_WERT_5 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_OFFSET_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_SLEEP_WERT_5 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_SLEEP_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KOMBI_RESET_5 | int | Anzahl Fahrten &gt;100 Km [Km] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _DATEN_1 | binary | daten1 |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _DATEN_2 | binary | daten2 |

<a id="job-status-historienspeicher-lesen-block-3"></a>
### STATUS_HISTORIENSPEICHER_LESEN_BLOCK_3

EnergieDatenSpeicher Teil e -Wecker IDs- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE3 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WECKER_CAN_ID_1 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_1 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_1 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_1 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_1 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_2 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_2 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_2 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_2 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_2 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_3 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_3 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_3 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_3 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_3 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_4 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_4 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_4 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_4 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_4 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_5 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_5 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_5 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_5 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_5 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_6 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_6 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_6 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_6 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_6 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_6 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_7 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_7 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_7 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_7 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_7 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_7 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_8 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_8 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_8 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_8 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_8 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_8 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_9 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_9 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_9 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_9 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_9 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_9 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_10 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_10 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_10 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_10 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_10 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_10 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_11 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_11 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_11 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_11 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_11 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_11 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_12 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_12 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_12 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_12 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_12 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_12 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_13 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_13 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_13 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_13 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_13 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_13 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_14 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_14 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_14 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_14 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_14 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_14 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_15 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_15 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_15 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_15 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_15 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_15 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_16 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_16 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_16 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_16 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_16 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_16 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_17 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_17 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_17 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_17 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_17 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_17 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_18 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_18 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_18 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_18 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_18 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_18 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_19 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_19 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_19 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_19 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_19 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_19 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_20 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_20 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_20 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_20 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_20 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_20 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_21 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_21 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_21 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_21 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_21 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_21 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_22 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_22 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_22 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_22 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_22 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_22 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_23 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_23 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_23 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_23 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_23 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_23 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_24 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_24 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_24 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_24 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_24 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_24 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_25 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_25 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_25 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_25 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_25 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_25 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_26 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_26 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_26 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_26 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_26 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_26 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_27 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_27 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_27 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_27 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_27 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_27 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_28 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_28 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_28 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_28 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_28 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_28 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_29 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_29 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_29 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_29 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_29 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_29 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_30 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_30 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_30 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_30 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_30 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_30 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_31 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_31 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_31 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_31 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_31 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_31 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_32 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_32 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_32 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_32 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_32 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_32 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_33 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_33 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_33 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_33 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_33 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_33 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_34 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_34 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_34 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_34 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_34 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_34 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_35 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_35 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_35 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_35 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_35 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_35 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_36 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_36 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_36 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_36 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_36 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_36 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_37 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_37 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_37 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_37 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_37 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_37 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_38 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_38 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_38 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_38 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_38 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_38 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_39 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_39 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_39 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_39 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_39 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_39 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_40 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_40 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_40 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_40 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_40 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_40 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_41 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_41 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_41 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_41 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_41 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_41 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_42 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_42 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_42 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_42 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_42 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_42 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_43 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_43 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_43 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_43 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_43 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_43 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_44 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_44 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_44 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_44 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_44 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_44 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_45 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_45 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_45 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_45 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_45 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_45 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_46 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_46 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_46 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_46 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_46 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_46 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_47 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_47 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_47 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_47 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_47 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_47 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_48 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_48 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_48 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_48 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_48 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_48 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_49 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_49 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_49 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_49 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_49 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_49 | string | Einheit fuer KM_STAND: KM |
| STAT_WECKER_CAN_ID_50 | unsigned int | Captured CAN ID |
| STAT_WECKER_CAN_ID_HEX_50 | string | Hex CAN ID Value |
| STAT_RELATIVZEIT_WERT_50 | unsigned long | Einheit fuer RELATIVZEIT: SEKUNDEN [s] |
| STAT_RELATIVZEIT_EINH_50 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_50 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_50 | string | Einheit fuer KM_STAND: KM |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _DATEN_1 | binary | daten1 |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _DATEN_2 | binary | daten2 |
| _TEL_AUFTRAG3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |
| _DATEN_3 | binary | daten3 |
| _TEL_AUFTRAG4 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG |
| _DATEN_4 | binary | daten4 |
| _TEL_AUFTRAG5 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT5 | binary | Hex-Antwort von SG |
| _DATEN_5 | binary | daten5 |

<a id="job-status-historienspeicher-lesen-detail-block-3"></a>
### STATUS_HISTORIENSPEICHER_LESEN_DETAIL_BLOCK_3

EnergieDatenSpeicher Teil e -Wecker IDs- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE3 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WECKER_CAN_ID | unsigned int | Captured CAN ID (Dec.) The 50 Entries are mapped on the Results STAT_WECKER_CAN_ID_xx (xx = 0,1,2,...) |
| STAT_WECKER_CAN_ID_HEX | string | Captured CAN ID (Hex.) The 50 Entries are mapped on the Results STAT_WECKER_CAN_ID_HEX_xx (xx = 0,1,2,...) |
| STAT_WECKER_SG_ANZAHL | int | Number of possible sender (ECU) for this CAN ID The 50 Entries are mapped on the Results STAT_WECKER_SG_ANZAHL_xx (xx = 0,1,2,...) |
| STAT_WECKER_SG_ID | unsigned int | Diagnostic address from sender The 50 Entries are mapped on the Results STAT_WECKER_SG_ID_xx (xx = 0,1,2,...) Depending on the number of possible sender (ECU) for this CAN ID (i = 1,2,...) i time following Results: (unsigned int)    STAT_WECKER_SG_ID_xx_i   dec. Diagnostic address from sender i |
| STAT_WECKER_SG_ID_HEX | string | Diagnostic address from sender (Hex value) The 50 Entries are mapped on the Results STAT_WECKER_SG_ID_HEX_xx (xx = 0,1,2,...) Depending on the number of possible sender (ECU) for this CAN ID (i = 1,2,...) i time following Results: (unsigned int)    STAT_WECKER_SG_ID_HEX_xx_i   dec. Diagnostic address from sender i |
| STAT_WECKER_SG_NAME | string | Name from sender The 50 Entries are mapped on the Results STAT_WECKER_SG_NAME_xx (xx = 0,1,2,...) Depending on the number of possible sender (ECU) for this CAN ID (i = 1,2,...) i time following Results: (string) STAT_WECKER_SG_NAME_xx_i   Name from sender i |
| STAT_RELATIVZEIT_WERT | unsigned long | Relative time [s] The 50 Entries are mapped on the Results STAT_RELATIVZEIT_WERT_xx (xx = 0,1,2,...) |
| STAT_KM_STAND_WERT | unsigned long | mileage [km] The 50 Entries are mapped on the Results STAT_KM_STAND_WERT_xx (xx = 0,1,2,...) |
| STAT_RELATIVZEIT_EINH | string | Einheit fuer RELATIVZEIT (alle Einträge): SEKUNDEN |
| STAT_KM_STAND_EINH | string | Einheit fuer KM_STAND (alle Einträge): KM |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _DATEN_1 | binary | daten1 |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _DATEN_2 | binary | daten2 |
| _TEL_AUFTRAG3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |
| _DATEN_3 | binary | daten3 |
| _TEL_AUFTRAG4 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG |
| _DATEN_4 | binary | daten4 |
| _TEL_AUFTRAG5 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT5 | binary | Hex-Antwort von SG |
| _DATEN_5 | binary | daten5 |

<a id="job-steuern-historienspeicher-loeschen"></a>
### STEUERN_HISTORIENSPEICHER_LOESCHEN

EnergieDatenSpeicher Teil 1 TEIL 2 und Teil 3 loeschen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE0 commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_MEM | string | Use 1 for Block 1, 2 for Block 2, 3 for Block 3 If "no parameter" all blocks will be deleted  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
| STAT_VERRIEGELUNG_DRITTE_SITZREIHE_EIN | int | Signal gueltig nur fuer: PL4 (E70) Dritte Sitzreihe Eingang Third Seat Row Input 0: KEINE BETÄTIGUNG, 1: TASTER GEDRÜCKT 0: NOT PUSHED, 1: PUSHED PIN 3, PORT P0.2 |
| STAT_MSA_TASTER_EIN | int | Signal gueltig nur fuer: PL2-Red MSA(Motor Start Automatisch) Taster MSA (Motor Start Automatic) Switch 0: KEINE BETÄTIGUNG, 1: TASTER GEDRÜCKT 0: NOT PUSHED, 1: PUSHED PIN 3, PORT P0.2 |
| STAT_EDC_TASTER_EIN | int | Signal gueltig nur fuer: PL2-Red (E90) EDC-Sport Taster EDC-Sport Switch 0: KEINE BETÄTIGUNG, 1: TASTER GEDRÜCKT 0: NOT PUSHED, 1: PUSHED PIN 3, PORT P0.2 |
| STAT_ZV_SICHERN_RELAIS_DIAG_EIN | int | Zentralverriegelung Sichern Relais Diagnose CentralLocking SECURE Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 14, PORT P0.11 |
| STAT_ZV_ENTRIEGELN_RELAIS_DIAG_EIN | int | Zentralverriegelung Entriegeln Relais Diagnose CentralLocking UnLOCK Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 13, PORT P0.10 |
| STAT_ZV_VERRIEGELN_RELAIS_DIAG_EIN | int | Zentralverriegelung Verriegeln Relais Diagnose CentralLocking LOCK Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 12, PORT P0.9 |
| STAT_ZV_SELEKTIV_ENTRIEGELN_RELAIS_DIAG_EIN | int | Zentralverriegelung selektives Verriegeln Relais Diagnose CentralLocking LOCKDRIVER Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 36, PORT P1.13 |
| STAT_KCAN_ERR_EIN | int | K-Can Fehler Meldung K-Can error indicator 0: NICHT AKTIV, 1: AKTIV 0: NOT ACTIVE, 1: ACTIVE Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 11,PORT P0.8 |
| STAT_KCAN_WAKE_EIN | int | KCAN Wake Up Signal KCAN Transceiver 0: NICHT AKTIV, 1: AKTIV 0: NOT ACTIVE, 1: ACTIVE Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 33, PORT P1.10 |
| STAT_PTWAKE_IN_EIN | int | PT-CAN Wake-up Eingang 0: NICHT AKTIV, 1: AKTIV 0: NOT ACTIVE, 1: ACTIVE CO_MICRO PIN 11,PORT D.7 |
| STAT_FH_FATH_GESCHW_SENSOR1_EIN | int | Fensterheber Fahrer hinten Motor Hallsensor 1 PowerWindow Reardriver Motor Hallsensor 1 0: AUS:0, 1: EIN (PULSIERT) 0: OFF:0, 1: ON  (PULSED) PIN 97, PORT P4.3 |
| STAT_FH_FATH_GESCHW_SENSOR2_EIN | int | Fensterheber Fahrer hinten Motor Hallsensor 2 PowerWindow Reardriver Motor Hallsensor 2 0: AUS:0, 1: EIN (PULSIERT) 0: OFF:0, 1: ON  (PULSED) PIN 104, PORT P4.10 |
| STAT_FH_BFTH_GESCHW_SENSOR1_EIN | int | Fensterheber Beifahrer hinten Motor Hallsensor 1 PowerWindow RearPassenger Motor Hallsensor 1 0: AUS:0, 1: EIN (PULSIERT) 0: OFF:0, 1: ON  (PULSED) PIN 95, PORT P4.1 |
| STAT_FH_BFTH_GESCHW_SENSOR2_EIN | int | Fensterheber Beifahrer hinten Motor Hallsensor 2 PowerWindow RearPassenger Motor Hallsensor 2 0: AUS:0, 1: EIN (PULSIERT) 0: OFF:0, 1: ON  (PULSED) PIN 35, PORT P1.12 |
| STAT_FH_FATH_AUF_DIAG_EIN | int | Fensterheber Fahrer hinten Auf-Relais Diag PowerWindow RearDriver OPEN Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 96, PORT P4.2 |
| STAT_FH_FATH_ZU_DIAG_EIN | int | Fensterheber Fahrer hinten Zu-Relais Diag PowerWindow RearDriver CLOSE Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 119, PORT P5.9 |
| STAT_FH_BFTH_AUF_DIAG_EIN | int | Fensterheber Beifahrer hinten Zu-Relais Diag PowerWindow RearPassenger OPEN Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 110, PORT P5.0 |
| STAT_FH_BFTH_ZU_DIAG_EIN | int | Fensterheber Beifahrer hinten Zu-Relais Diag PowerWindow RearPassenger CLOSE Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 112, PORT P5.2 |
| STAT_HECKWISCHER_DIAG_EIN | int | Heckwischer Relais Diagnose Rear Wiper Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 2,PORT P0.1 |
| STAT_FRONTWISCHER_DIAG_EIN | int | Frontwischer Ein/Aus Relais Diagnose FrontWiper Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 57, PORT P2.10 |
| STAT_FRONTWISCHER_GESCHW_DIAG_EIN | int | Frontwischer Geschwingdigkeit Relais Diagnose FrontWiper Speed Relay Diagnosis 0: Relais Abgeschaltet, 1: Relais Eingeschaltet 0: LOW, 1: HIGH PIN 58, PORT P2.11 |
| STAT_FRONTWISCHER_RSK_EIN | int | Frontwischer Rückstellkontakt Front Wiper Park Position 0: FrontWischer nicht im RSK, 1: FrontWischer im RSK 0: Wiper Not in Park Position, 1: Wiper in Park Position Wert am Pin umgekehrt! Actual Value Inverted! PIN 134, PORT P6.5 |
| STAT_HECKWISCHER_RSK_EIN | int | Signal nicht gueltig fuer: PL2-Red (E88) Heckwischer Rückstellkontakt Rear Wiper Park Position 0: HeckWischer nicht im RSK, 1: HeckWischer im RSK 0: Wiper Not in Park Position, 1: Wiper in Park Position Wert am Pin umgekehrt! Actual Value Inverted! PIN 121, PORT P5.11 |
| STAT_VERDECK_KONTAKT_EIN | int | Signal gueltig nur fuer: PL2-Red (E88) Verdeck Kontakt Manual Convertible Top Contact 0: Geschlossen, 1: Offen 0: Closed, 1: Open PIN 121, PORT P5.11 |
| STAT_SRA_DIAG_EIN | int | Scheinwerferreinigung Relais Diagnose HeadlampWasher Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 18, PORT P0.13 |
| STAT_KUEHLMITTELSTAND_EIN | int | Kühlmittelstand 0: Zu niedriger Füllstand, 1: Normaler Füllstand Cooling Level Sensor 0: UNDER LEVEL, 1: NORMAL Wert am Pin umgekehrt! Actual Value Inverted! PIN 124, PORT P5.14 |
| STAT_WASCHWASSERSTAND_EIN | int | Waschwasserstand 0: Zu niedriger Füllstand, 1: Normaler Füllstand Water Level Sensor 0: UNDER LEVEL, 1: NORMAL Wert am Pin umgekehrt! Actual Value Inverted! PIN 139, PORT P6.10 |
| STAT_DSC_BEFEHL_EIN | int | DSC(dynamische Stabilität Kontrolle)Taster Eingang DSC (Dynamic stability control) Switch input 0: Keine Betätigung, 1:Taster Gedrückt 0: Not Pushed, 1: Pushed PIN 94, PORT P4.0 |
| STAT_5V_SW_DIAG_EIN | int | Diagnose atmel 5v_sw von der Aktivierung Diagnostics from atmel 5v_sw activation Nicht im Gebrauch. Es sollte immer 0 sein Not in Use. Should be always 0 Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 130, PORT P6.1 |
| STAT_EVV_HS_DIAG_EIN | int | Diagnose von electronische Volumenstrom-Ventil (EVV) High Side FET Servotronic (EVV) High Side FET Diagnosis 0: Überlastung oder Übertemperatur, 1: Normalbetrieb 0: Overload or Overtemperature, 1: Normal Operation Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 34, PORT P1.11 |
| STAT_EVV_LS_DIAG_EIN | int | Diagnose von electronische Volumenstrom-Ventil (EVV) Low Side FET Servotronic (EVV) Low Side FET Diagnosis 0: NICHT AKTIV, 1: AKTIV 0: NOT ACTIVE, 1: ACTIVE Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 106, PORT P4.12 |
| STAT_HECKSCHEIBENHEIZUNG_DIAG_EIN | int | Heckscheibenheizung Relais Diagnose Rearwindow Heater Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON PIN 131, PORT P6.2 |
| STAT_HANDBREMSE_KONTAKT_EIN | int | Handbremsekontakt 0: Gelöst, 1: Angezogen Handbrake Contact Input 0: Not Active, 1: Active PIN 132, PORT P6.3 |
| STAT_HECKKLAPPE_KONTAKT_EIN | int | Hecklappenkontakt Trunklid Contact 0: Geschlossen, 1: Offen 0: Closed, 1: Open CO_MICRO PIN 12,PORT B.0 |
| STAT_HECKKLAPPE_TASTER_EIN | int | Taster Entriegeln Heckklappe Trunklid External Switch 0: Keine Betätigung, 1: Taster Gedrückt 0: Not pushed, 1: Pushed CO_MICRO PIN 7,PORT B.6 |
| STAT_HECKKLAPPE_DIAG_EIN | int | Heckklappe Relais Diagnose Trunklid Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 9,PORT P D.5 |
| STAT_HECKSCHEIBE_KONTAKT_EIN | int | Heckscheibenkontakt RearWindow Button Contact 0: Geschlossen, 1: Offen 0: Closed, 1: Open CO_MICRO PIN 13,PORT B.1 |
| STAT_HECKSCHEIBE_TASTER_EIN | int | Signal gueltig nur fuer: PL2-RED Entriegeln Heckscheibe Taster RearWindow Unlock External Switch 0: Keine Betätigung, 1: Taster Gedrückt 0: Not pushed, 1: Pushed CO_MICRO PIN 10,PORT D.6 |
| STAT_HECKSCHEIBE_DIAG_EIN | int | Heckbistabiles Relais Diagnose RearBistable Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 2,PORT D.4 |
| STAT_HANDSCHUHKASTEN_KONTAKT_EIN | int | Signal gueltig nur fuer: PL4 (E70) und PL2-RED (E93) Handschuhkasten Taster GloveBox External Switch 0: Keine Betätigung, 1: Taster Gedrückt 0: Not pushed, 1: Pushed CO_MICRO PIN 10,PORT D.6 |
| STAT_HANDSCHUHKASTEN_DIAG_EIN | int | Signal gueltig nur fuer: PL4 (E70) und PL2-RED (E93) Handschuhkasten Relais Diagnose GloveBox Relay Diagnosis 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 136, PORT P6.7 |
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
| STAT_ZV_SICHERN_RELAIS_EIN | int | Zentralverriegelung Sichernrelais CentralLocking SECURE Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 22,PORT P1.1 |
| STAT_ZV_ENTRIEGELN_RELAIS_EIN | int | Zentralverriegelung Entriegelnrelais CentralLocking UNLOCK Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 8,PORT P0.5 |
| STAT_ZV_VERRIEGELN_RELAIS_EIN | int | Zentralverriegelung Verriegelnrelais CentralLocking LOCK Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 32,PORT P1.9 |
| STAT_ZV_SELEKTIV_ENTRIEGELN_RELAIS_EIN | int | Zentralverriegelung selektiv Entriegelnrelais CentralLocking LOCK DRIVER Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 31,PORT P1.8 |
| STAT_ZV_AUSGANG_EIN | int | Zentralverriegelung Ausgang CentralLocking Output 0x00: Aus, 2: Entriegeln(ER), 6: Selektiv Entriegeln(SER), 12: Verriegeln(VR), 13: Sichern(VRZS), 14: Entsichern(ES) 0x00: OFF, 2: UNLOCK, 6: SELECTIVE, 12: LOCK, 13: SECURE, 14: UNSECURE |
| STAT_FH_FATH_AUF_EIN | int | Fensterheber Fahrer Hinten Auf (Relaissteuerung) PowerWindow RearDriver OPEN Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 24,PORT P1.3 |
| STAT_FH_FATH_ZU_EIN | int | Fensterheber Fahrer Hinten Zu (Relaissteuerung) PowerWindow RearDriver CLOSE Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 29,PORT P1.6 |
| STAT_FH_FATH_AUSGANG_EIN | int | Fensterheber Fahrer Hinten (Relaissteuerung) PowerWindow RearDriver Output 0: AUS, 1: AUF, 2: ZU 0: OFF, 1: DOWN, 2: UP |
| STAT_FH_BFTH_AUF_EIN | int | Fensterheber Beifahrer Hinten Auf (Relaissteuerung) PowerWindow RearPassenger OPEN Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 20,PORT P0.15 |
| STAT_FH_BFTH_ZU_EIN | int | Fensterheber Beifahrer Hinten Zu (Relaissteuerung) PowerWindow RearPassenger CLOSE Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 21,PORT P1.0 |
| STAT_FH_BFTH_AUSGANG_EIN | int | Fensterheber Beifahrer Hinten (Relaissteuerung) PowerWindow RearPassenger Output 0: AUS, 1: AUF, 2: ZU 0: OFF, 1: DOWN, 2: UP |
| STAT_FH_CHIPSELECT_EIN | int | Chip select signal for E.100_47 0: DISABLE, 1: ENABLE Internes Signal der JBBF Not External JBBF Input PIN 123,PORT P5.13 |
| STAT_FH_WAKE_EIN | int | Fenterheber Aufwachen Steuerung PowerWindow Wake Control 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 133,PORT P6.4 |
| STAT_VERDECKKASTENSCHLOSS_EIN | int | Signal gueltig nur fuer: PL2-RED (E88) Verdeckkastenschloss Manual Convertible Top Unlock Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 1,PORT P0.0 |
| STAT_HECKWISCHER_EIN | int | Signal gueltig nur fuer: PL4 (E70) Heckwischer (Relaissteuerung) RearWiper Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 1,PORT P0.0 |
| STAT_FRONTWISCHER_EIN | int | Frontwischer Ein/Aus (Relaissteuerung) FrontWiper Relay (Low Speed Relay) 0: AUS, 1: EIN 0: OFF, 1: ON PIN 137, PORT P6.8 |
| STAT_FRONTWISCHER_GESCHW_EIN | int | Frontwischer Geschwingdigkeit (Relaissteuerung) FrontWiper Speed Relay (High Speed Relay) 0: AUS, 1: EIN 0: OFF, 1: ON PIN 4, PORT P0.3 |
| STAT_FRONTWISCHER_AUSGANG_EIN | int | Frontwischer (Relaissteuerung) FrontWiper Output 0: Aus, 1: Stufe 1 (Langsam) (PL2 Kompatibilitaet), 3: Stufe 2(Schnell) 0: OFF, 1: STATE 1 (Slow) (PL2 compatibility), 3: STATE 2(Fast) |
| STAT_SRA_EIN | int | Scheinwerferreinigungsanlage (Relaissteuerung) HeadLamp Washer Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 7,PORT P0.4 |
| STAT_ZUSATZWASSERPUMPE_EIN | int | Zusätzlicher Wasser-Pumpe Additional WaterPump 0: AUS, 1: EIN 0: OFF, 1: ON PIN 105,PORT P4.11 |
| STAT_HECKWASCHERPUMPE_EIN | int | Heckwascher Pumpe RearWasher Pump 0: AUS, 1: EIN 0: OFF, 1: ON PIN 101,PORT P4.7 |
| STAT_FRONTWASCHERPUMPE_EIN | int | Frontwascher Pumpe FrontWasher Pump 0: AUS, 1: EIN 0: OFF, 1: ON PIN 100,PORT P4.6 |
| STAT_WASSERVENTIL_FAHRER_OFFEN | int | Wasser-Ventil 1 (Fahrer) Ansteuerung. Pin Wert Water Valve 1 (Driver) Control. Pin value 0: GESCHLOSSEN, 1: OFFEN 0: CLOSED, 1: OPEN PIN 120,PORT P5.10 |
| STAT_WASSERVENTIL_BEIFAHRER_OFFEN | int | PL4 (E70): Wasser-Ventil 2 (Beifahrer) Ansteuerung. Pin Wert Water Valve 2 (Passenger) Control. Pin value PL2-RED (E90_M3): EDC-Sport Switch Led 2 Indicator 0: GESCHLOSSEN, 1: OFFEN 0: CLOSED, 1: OPEN PIN 102,PORT P4.8 |
| STAT_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_AUSGANG_EIN | int | Waschdüsenheizung und Aussenspiegel JetWasher and Mirror Heating 0: AUS, 3: BEIDES EIN (aus historischen Gründe - PL2 Kompatibilitaet) 0: OFF, 3: ON (due to historical reasons - PL2 compatibility) PIN 138,PORT P6.9 |
| STAT_MAG_KUP_EIN | int | Magnetisch Kupplung Magnetic Kupplung 0: AUS, 1: EIN 0: OFF, 1: ON PIN 111,PORT P5.1 |
| STAT_EVV_LS_EIN | int | electronische Volumenstrom-Ventil (EVV) Low Side FET Ausgang Servotronic (EVV) Low Side FET Output 0: AUS, 1: EIN 0: OFF, 1: ON PIN 135,PORT P6.6 |
| STAT_SONNENROLLO_LOWTREIBER1_EIN | int | PL2-RED (E90,E92): Sonnenrollo Lowtreiber 1 SunBlind Mosfet LowSide 1 PL4 (E70): Handschuhkasten Entriegelung GloveBox Unlock 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 42,PORT P2.3 |
| STAT_SONNENROLLO_LOWTREIBER2_EIN | int | PL2-RED (E90,E92): Sonnenrollo Lowtreiber 2 SunBlind Mosfet LowSide 2 PL2-RED (E91): Trunkcover Laderraumabdeckung PL2-RED (E93): Handschuhkasten Entriegelung GloveBox Unlock 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 44,PORT P2.5 |
| STAT_SONNENROLLO_HIGHTREIBER1_EIN | int | PL2-RED (E90,E92): Sonnenrollo Hightreiber 1 SunBlind Mosfet HighSide 1 PL4 (E70) Handschuhkasten Entriegelung GloveBox Unlock 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 125,PORT P5.15 |
| STAT_SONNENROLLO_HIGHTREIBER2_EIN | int | PL2-RED (E90,E92): Sonnenrollo Hightreiber 2 SunBlind Mosfet HighSide 2 PL2-RED (E91): Trunkcover Laderraumabdeckung PL2-RED (E93): Handschuhkasten Entriegelung GloveBox Unlock 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBF Not External JBBF Input PIN 28,PORT P1.5 |
| STAT_SONNENROLLO_AUSGANG_EIN | int | PL2-RED (E90,E92): Sonnenrollo Ausgang Sunblind Output 0: Aus, 5: Von Ein zu Aus, 6: Nach oben, 9: Herunter 0: OFF, 5: ON2OFF, 6: UP, 9: DOWN |
| STAT_HANDSCHUHKASTEN_E70_EIN | int | Signal gueltig nur fuer: PL4 (E70) Handschuhkasten Entriegelung GloveBox Unlock 400 ms default Activation Time 0: AUS, 1: EIN 0: OFF, 1: ON PIN 125,PORT P5.15 |
| STAT_LADERRAUMABDECKUNG_AUSGANG_EIN | int | Signal gueltig nur fuer: PL2-Red (E91) Laderraumabdeckung Trunkcover 2 sec Activation Time to complete open 0: AUS, 1: EIN 0: OFF, 1: ON |
| STAT_HECKSCHEIBENHEIZUNG_EIN | int | Heckscheibenheizung (Relaissteuerung) Rear Window Heater Relay 0: AUS, 1: EIN 0: OFF, 1: ON PIN 10,PORT P0.7 |
| STAT_HECKKLAPPE_EIN | int | PL4 (E70): Heckklappe Relais / SCA (Relaissteuerung) TrunkLid Unlock Relay / SCA PL2-RED: Heckklappe Relais (Relaissteuerung) TrunkLid Unlock Relay 0: LOCK, 1: UNLOCK PIN 107,PORT P4.13 |
| STAT_HECKSCHEIBE_EIN | int | Heckscheibe (Relaissteuerung) RearWindow Unlock Relay 0: AUS, 1: EIN 0: LOCK, 1: UNLOCK PIN 109,PORT P4.15 |
| STAT_BISTABILRELAIS_ON_EIN | int | Bistabiles Relais ON Bistable Relay ON 100 ms max. Activation Time 0: AUS, 1: EIN 0: OFF, 1: ON PIN 9,PORT P0.6 |
| STAT_BISTABILRELAIS_OFF_EIN | int | Bistabiles Relais OFF Bistable Relay OFF 100 ms max. Activation Time 0: AUS, 1: EIN 0: OFF, 1: ON PIN 61,PORT P2.14 |
| STAT_HECKBISTABILRELAIS_ON_EIN | int | Heckbistabiles Relais ON RearBistable Relay ON 100 ms max. Activation Time 0: AUS, 1: EIN 0: OFF, 1: ON PIN 108,PORT P4.14 |
| STAT_HECKBISTABILRELAIS_OFF_EIN | int | Heckbistabiles Relais OFF RearBistable Relay OFF 100 ms max. Activation Time 0: AUS, 1: EIN 0: OFF, 1: ON PIN 113,PORT P5.3 |
| STAT_5V_SW_ON_EIN | int | Überschreibt atmel 5V_SW. Freigabe internal Versorgungsspannung Overwrites atmel 5V_SW 0: AUS, 1: EIN 0: OFF, 1: ON Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 62,PORT P2.15 |
| STAT_KCAN_ENABLE_EIN | int | Enable KCAN transceiver TJA1054 0: DISABLE, 1: ENABLE Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 23,PORT P1.2 |
| STAT_KCAN_STB_EIN | int | Standby KCAN transceiver TJA1054 0: DISABLE, 1: ENABLE Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 27,PORT P1.4 |
| STAT_HIGHSPEEDCAN_ENABLE_EIN | int | High Speed CAN Transceiver (TJA1040) Enable 0: ENABLE, 1: DISABLE Internes Signal der JBBF Not External JBBF Input PIN 60,PORT P2.13 |
| STAT_DIAGCAN_ENABLE_EIN | int | Diagnosis CAN Transceiver (TJA1040) Enable 0: ENABLE, 1: DISABLE Internes Signal der JBBF Not External JBBF Input PIN 122,PORT P5.12 |
| STAT_KL30SW_ENABLE_EIN | int | KL30SW befähigen (Relaissteuerung) KL30SW Enable 0: DISABLE, 1: ENABLE Internes Signal der JBBF Not External JBBF Input PIN 59,PORT P2.12 |
| STAT_TANKSENSOREN_ENABLE_EIN | int | FuelTank Sensoren befähigen Fuel Tank Enable 0: DISABLE, 1: ENABLE Internes Signal der JBBF Not External JBBF Input PIN 103,PORT P4.9 |
| STAT_PTWAKE_OUT_EIN | int | PT-CAN Wake UP Pulse 0: NICHT AKTIV, 1: AKTIV 0: NOT ACTIVE, 1: ACTIVE PIN 118,PORT P5.8 |
| STAT_5V_SENSOR_ENABLE_EIN | int | 5V SENSOR befähigen 5V SENSOR Enable 0: DISABLE, 1: ENABLE PIN 129,PORT P6.0 |
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
| STAT_ADC_BATTERIE_SPANNUNG_WERT | int | Digital Wandler Wert von Batterie Spannung Sensor Digital converted value from Battery Voltage Sensor (HEX) Wertbereich: 0..0x3FF (1023) PIN 67,PORT P3.0 |
| STAT_BATTERIE_SPANNUNG_WERT | real | Batterie Spannung Battery Voltage (Vbat) [V] Wertbereich: 0..28.40 [V] Aufloesung (Resolution): 0,0277 V/Bit, for Vref=5V Vbat=(HEX)*100/3605 PIN 67,PORT P3.0 |
| STAT_BATTERIE_SPANNUNG_EINH | string | Einheit fuer Batterie Spannung: Volt |
| STAT_ADC_FH_FATH_SCHALTER_WERT | int | Digital Wandler Wert von Fensterheber Fahrer Hinten Schalter (lokaler Taster) Digital converted value from PowerWindow Rear-Driver Button (local switch) Wertbereich: 0..0x3FF(1023) 143(0x08F)....346(0x15A) : DOWNAUTO(2) 347(0x15B)....571(0x23B) : DOWNMANUAL(1) 572(0x23C)....756(0x2F4) : UPAUTO(4) 757(0x2F5)....951(0x3B7) : UPMANUAL(3) 952(0x3B8)....1023(0x3FF): OFF(0) PIN 69,PORT P3.2 |
| STAT_FH_FATH_SCHALTER_WERT | int | Fensterheber Fahrer Hinten Schalter (lokaler Taster) PowerWindow Rear-Driver Button (local switch) 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) PIN 69,PORT P3.2 |
| STAT_FH_FATH_SCHALTER_TEXT | string | Fensterheber Fahrer Hinten Schalter (lokaler Taster) PowerWindow Rear-Driver Button (local switch) Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 PIN 69,PORT P3.2 |
| STAT_ADC_FH_BFTH_SCHALTER_WERT | int | Digital Wandler Wert von Fensterheber Beifahrer Hinten Schalter (lokaler Taster) Digital converted value from PowerWindow Rear-Passenger Button (local switch) Wertbereich: 0..0x3FF(1023) 143(0x08F)....346(0x15A) : DOWNAUTO(2) 347(0x15B)....571(0x23B) : DOWNMANUAL(1) 572(0x23C)....756(0x2F4) : UPAUTO(4) 757(0x2F5)....951(0x3B7) : UPMANUAL(3) 952(0x3B8)....1023(0x3FF): OFF(0) PIN 68,PORT P3.1 |
| STAT_FH_BFTH_SCHALTER_WERT | int | Fensterheber Beifahrer Hinten Schalter (lokaler Taster) PowerWindow Rear-Passenger Button (local switch) 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) PIN 68,PORT P3.1 |
| STAT_FH_BFTH_SCHALTER_TEXT | string | Fensterheber Beifahrer Hinten Schalter (lokaler Taster) PowerWindow Rear-Passenger Button (local switch) Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 PIN 68,PORT P3.1 |
| STAT_ADC_FH_BFT_SCHALTER_WERT | int | Digital Wandler Wert von Fensterheber Beifahrer Schalter (lokaler Taster) Digital converted value from PowerWindow Passenger Button (local switch) Wertbereich: 0..0x3FF(1023) 143(0x08F)....346(0x15A) : DOWNAUTO(2) 347(0x15B)....571(0x23B) : DOWNMANUAL(1) 572(0x23C)....756(0x2F4) : UPAUTO(4) 757(0x2F5)....951(0x3B7) : UPMANUAL(3) 952(0x3B8)....1023(0x3FF): OFF(0) PIN 73,PORT P3.6 |
| STAT_FH_BFT_SCHALTER_WERT | int | Fensterheber Beifahrer Schalter (lokaler Taster) PowerWindow Passenger Button (local switch) 0: Taster nicht gedrueckt (OFF) 1: Manuell oeffnen	      (DOWNMANUAL) 2: Maut. oeffnen	   	  (DOWNAUTO) 3: Manuell schliessen	  (UPMANUAL) 4: Maut. schliessen		  (UPAUTO) PIN 73,PORT P3.6 |
| STAT_FH_BFT_SCHALTER_TEXT | string | Fensterheber Beifahrer Schalter (lokaler Taster) PowerWindow Passenger Button (local switch) Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 PIN 73,PORT P3.6 |
| STAT_ADC_TANK_LI_FUELLSTAND_WERT | int | Digital Wandler Wert von Fuel Tank Links Digital converted value from Fuel Tank Level Sensor Left Wertbereich: 0..0x3FF(1023) PIN 70,PORT P3.3 |
| STAT_TANK_LI_WIDERSTAND_WERT | real | Widerstand Fuel Tank Links Resistance Fuel Tank Level Sensor Links Wertebereich:(0,244&lt;signal&lt;4,145) MIN:0x032, MAX:0x350, Gültig: 0..1207 [Ohm], 0xFFFF OFFENE-LAST Range of values:(0,244&lt;signal&lt;4,145) MIN:0x032, MAX:0x350, Valid: 0..1207 [Ohm], 0xFFFF OPEN-LOAD PIN 70,PORT P3.3 |
| STAT_TANK_LI_WIDERSTAND_EINH | string | Einheit fuer Widerstand Fuel Tank: Ohm |
| STAT_ADC_TANK_RE_FUELLSTAND_WERT | int | Digital Wandler Wert von Fuel Tank Rechts Digital converted value from Fuel Tank Level Sensor Right Wertbereich: 0..0x3FF(1023) PIN 71,PORT P3.4 |
| STAT_TANK_RE_WIDERSTAND_WERT | real | Widerstand Fuel Tank Rechts Resistance Fuel Tank Level Sensor Right Wertebereich:(0,244&lt;signal&lt;4,145) MIN:0x032, MAX:0x350, Gültig: 0..1207 [Ohm], 0xFFFF OFFENE-LAST Range of values:(0,244&lt;signal&lt;4,145) MIN:0x032, MAX:0x350, Valid: 0..1207 [Ohm], 0xFFFF OPEN-LOAD PIN 71,PORT P3.4 |
| STAT_TANK_RE_WIDERSTAND_EINH | string | Einheit fuer Widerstand Fuel Tank: Ohm |
| STAT_ADC_EVV_SENSE_WERT | int | Digital Wandler Wert von electronische Volumenstrom-Ventil (EVV) Ausgang Strom Sensor Digital converted value from Servotronic (EVV) Output Current Sensor Wertbereich: 0..0x3FF(1023) Range of values: 0..0x3FF(1023) Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 72,PORT P3.5 |
| STAT_EVV_SENSE_WERT | int | electronische Volumenstrom-Ventil (EVV) Ausgang Strom Sensor Servotronic Output Current Sensor Wertbereich: 100mA ..1000 mA Range of values: 100mA...1000mA Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 72,PORT P3.5 |
| STAT_EVV_SENSE_EINH | int | Einheit fuer EVV VENTIL: mA Current Units: mA |
| STAT_ADC_DRUCKSENSOR_WERT | int | Digital Wandler Wert von Druck-Sensor Digital converted value from Pressure Sensor Wertebereich: 0  &lt; Signal &lt; 1023 (10 bit ADC) Range of values: 0 &lt; signal &lt;1023 (10 bit ADC) PIN 74,PORT P3.7 |
| STAT_DRUCKSENSOR_WERT | int | Druck-Sensor Pressure Sensor Wertebereich: 0 &lt; Signal &lt; 127.5 Bar Range of values: 0 &lt; Signal &lt; 127.5 Bar PIN 74,PORT P3.7 |
| STAT_DRUCKSENSOR_EINH | string | Einheit fuer Drucksensor: Bar |
| STAT_WASCHERPUMPE_DIAG_WERT | int | Wascherpumpe Diagnose WasherPump Diagnosis Wertebereich: 0.2 &lt; Signal &lt; 4,5V MIN:0x029, MAX:0x398 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4,5V MIN:0x029, MAX:0x398 valid: 0..0x3FF, 0xFFFF signal invalid PIN 77 PORT P3.8 |
| STAT_ADC_FATH_KL30_SENSE_WERT | int | Signal gueltig nur fuer: PL4 (E70) Digital Wandler Wert von Fensterheber Fahrer Hinten Motor Sense Digital converted value from PowerWindow Rear-Driver Motor Sense (HEX) Wertbereich: 0..0x3FF (1023) PIN 78,PORT P3.9 |
| STAT_FATH_KL30_SENSE_WERT | real | Signal gueltig nur fuer: PL4 (E70) Fahrer Hinten Motor Sense Rear-Driver Motor Sense Wertbereich: 0..28.40 [Volt] Aufloesung (Resolution): 0,0277 V/Bit, for Vref=5V Vbat=(HEX)*100/3605 PIN 78,PORT P3.9 |
| STAT_FATH_KL30_SENSE_EINH | string | Einheit fuer Fahrer Hinten Motor Sense: Volt |
| STAT_ADC_BFTH_KL30_SENSE_WERT | int | Signal gueltig nur fuer: PL4 (E70) Digital Wandler Wert von Fensterheber Beifahrer Hinten Motor Sense Digital converted value from PowerWindow Rear-Passenger Motor Sense (HEX) Wertbereich: 0..0x3FF (1023) PIN 79,PORT P3.10 |
| STAT_BFTH_KL30_SENSE_WERT | real | Signal gueltig nur fuer: PL4 (E70) Beifahrer Hinten Motor Sense Rear-Passenger Motor Sense Wertbereich: 0..28.40 [Volt] Aufloesung (Resolution): 0,0277 V/Bit, for Vref=5V Vbat=(HEX)*100/3605 PIN 79,PORT P3.10 |
| STAT_BFTH_KL30_SENSE_EINH | string | Einheit fuer Beifahrer Hinten Motor Sense: Volt |
| STAT_KOMPRESSOR_DIAG_WERT | int | Diagnose Wechselstrom Kompressor des Ausganges Kompressor output Diagnosis Wertebereich: 0.2 &lt; Signal &lt; 4V MIN:0x029, MAX:0x333 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4V MIN:0x029, MAX:0x333 valid: 0..0x3FF, 0xFFFF signal invalid Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 80,PORT P3.11 |
| STAT_ADC_SONNENROLLO_STROM_WERT | int | Digital Wandler Wert von Sonnenrollo Strom Sensor Digital converted value from Sunblind Current Sensor Wertebereich: 0.2 &lt; Signal &lt; 4V MIN:0x029, MAX:0x333 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4V MIN:0x029, MAX:0x333 valid: 0..0x3FF, 0xFFFF signal invalid Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 81,PORT P3.12 |
| STAT_SONNENROLLO_STROM_WERT | real | Sonnenrollo Strom Sensor Wertebereich: 0..12 [A] (PH)=12.2775*HEX/1024, for Vref=5V Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 81,PORT P3.12 |
| STAT_SONNENROLLO_STROM_EINH | string | Einheit fuer Sonnenrollo: Amp |
| STAT_KOMPRESSOR_KUPPLUNG_DIAG_WERT | int | Magnet Kupplung Diagnose AC Clutch Diagnosis Wertebereich: 0.2 &lt; Signal &lt; 4,5V MIN:0x029, MAX:0x398 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4,5V MIN:0x029, MAX:0x398 valid: 0..0x3FF, 0xFFFF signal invalid Internes Signal der JBBFE2 Not External JBBFE2 Input PIN 82,PORT 3.13 |
| STAT_ADC_FONDSCHICHTUNGSENSOR_WERT | int | Digital Wandler Wert von Fond Schichtung-Sensor Digital converted value from Rear Air Flow Sensor Wertebereich: 0  &lt; Signal &lt; 1023 (10 bit ADC) Range of values: 0 &lt; signal &lt;1023(10 bit ADC) PIN 83,PORT P3.14 |
| STAT_FONDSCHICHTUNGSENSOR_WERT | int | Schichtung Fondschichtung Sensor Opening Rear Air Flow Sensor Wertebereich: 0&lt; Signal &lt; 100 Range of values: 0 &lt; signal &lt; 100 PIN 83,PORT P3.14 |
| STAT_FONDSCHICHTUNGSENSOR_EINH | string | Einheit fuer Fondschichtungsensor: % |
| STAT_ADC_5V_SENSOR_DIAG_WERT | int | Diagnose des 5V Sensor (Druck Sensor Versorgunsspannung) 5V Sensor (Pressure Sensor Supply) Diagnosis Aufloesung (Resolution): 4.88 mV/Bit, for Vref=5V Wertbereich: 0..0x3FF(1023) Range of values: 0..0x3FF(1023) PIN 84,PORT P3.15 |
| STAT_ADC_FH_FATH_MFFHA_STROM_SENSE_WERT | int | Signal gueltig nur fuer: PL2-RED (E93) Digital Wandler Wert von Fensterheber Fahrer Hinten Strom Sense Auf Relais Digital converted value from PowerWindow Rear-Driver Current Sense Open Relay (HEX) PW_SENSE_1 Wertbereich: 0..0x3FF (1023) Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 28,PORT C.5 |
| STAT_FH_FATH_MFFHA_STROM_SENSE_WERT | real | Signal gueltig nur fuer: PL2-RED (E93) Fahrer Hinten Strom Sense Auf Relais Rear-Driver Current Sense Open Relay (HEX) PW_SENSE_1 Wertbereich: Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 28,PORT C.5 |
| STAT_FH_FATH_MFFHA_STROM_SENSE_EINH | string | Einheit fuer Fahrer Hinten Strom Sense Auf Relais: Amp |
| STAT_ADC_FH_FATH_MFFHZ_STROM_SENSE_WERT | int | Signal gueltig nur fuer: PL2-RED (E93) Digital Wandler Wert von Fensterheber Fahrer Hinten Strom Sense Zu Relais Digital converted value from PowerWindow Rear-Driver Current Sense Close Relay (HEX) PW_SENSE_2 Wertbereich: 0..0x3FF (1023) Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 23,PORT C.0 |
| STAT_FH_FATH_MFFHZ_STROM_SENSE_WERT | real | Signal gueltig nur fuer: PL2-RED (E93) Fahrer Hinten Strom Sense Zu Relais Rear-Driver Current Sense Close Relay (HEX) PW_SENSE_2 Wertbereich: Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 23,PORT C.0 |
| STAT_FH_FATH_MFFHZ_STROM_SENSE_EINH | string | Einheit fuer Fahrer Hinten Strom Sense Zu Relais: Amp |
| STAT_ADC_FH_BFTH_MFBHA_STROM_SENSE_WERT | int | Signal gueltig nur fuer: PL2-RED (E93) Digital Wandler Wert von Fensterheber Beifahrer Hinten Strom Sense Auf Relais Digital converted value from PowerWindow Rear-Passenger Current Sense Open Relay (HEX) PW_SENSE_3 Wertbereich: 0..0x3FF (1023) Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 22,PORT ADC7 |
| STAT_FH_BFTH_MFBHA_STROM_SENSE_WERT | real | Signal gueltig nur fuer: PL2-RED (E93) Beifahrer Hinten Strom Sense Auf Relais Rear-Passenger Current Sense Open Relay (HEX) PW_SENSE_3 Wertbereich: Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 22,PORT ADC7 |
| STAT_FH_BFTH_MFBHA_STROM_SENSE_EINH | string | Einheit fuer Beifahrer Hinten Strom Sense 2: Amp |
| STAT_ADC_FH_BFTH_MFBHZ_STROM_SENSE_WERT | int | Signal gueltig nur fuer: PL2-RED (E93) Digital Wandler Wert von Fensterheber Beifahrer Hinten Strom Sense Zu Relais Digital converted value from PowerWindow Rear-Passenger Current Sense Close Relay (HEX) PW_SENSE_4 Wertbereich: 0..0x3FF (1023) Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 24,PORT C.1 |
| STAT_FH_BFTH_MFBHZ_STROM_SENSE_WERT | real | Signal gueltig nur fuer: PL2-RED (E93) Beifahrer Hinten Strom Sense Zu Relais Rear-Passenger Current Sense Close Relay (HEX) PW_SENSE_4 Wertbereich: Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 24,PORT C.1 |
| STAT_FH_BFTH_MFBHZ_STROM_SENSE_EINH | string | Einheit fuer Beifahrer Hinten Strom Sense 2: Amp |
| STAT_WASSERVENTIL_FAHRER_DIAG_WERT | int | Wasserventil 1 (Fahrer) Diagnose Water Valve 1 (Driver) Diagnosis Wertebereich: 0.2 &lt; Signal &lt; 4,5V MIN:0x029, MAX:0x398 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4,5V MIN:0x029, MAX:0x398 valid: 0..0x3FF, 0xFFFF signal invalid Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 25,PORT C.2 |
| STAT_WASSERVENTIL_BEIFAHRER_DIAG_WERT | int | Wasserventil 2  (Beifahrer) Diagnose Water Valve 2 (Passenger) Diagnosis Wertebereich: 0.2 &lt; Signal &lt; 4,5V MIN:0x029, MAX:0x398 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4,5V MIN:0x029, MAX:0x398 valid: 0..0x3FF, 0xFFFF signal invalid Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 27,PORT C.4 |
| STAT_ZUSATZWASSERPUMPE_DIAG_WERT | int | Zusatzwasserpumpe Diagnose Additional Water Pump Diagnosis Wertebereich: 0.2 &lt; Signal &lt; 4,5V MIN:0x029, MAX:0x398 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4,5V MIN:0x029, MAX:0x398 valid: 0..0x3FF, 0xFFFF signal invalid Internes Signal der JBBFE2 Not External JBBFE2 Input CO_MICRO PIN 26,PORT C.3 |
| STAT_WASCHDUESENHEIZUNG_DIAG_WERT | int | Waschduesenheizung Diagnose JetWasher Heater Diagnosis Wertebereich: 0.2 &lt; Signal &lt; 4,5V MIN:0x029, MAX:0x398 Gültig: 0..0x3FF,  0xFFFF Signal ungültig Range of values: 0.2 &lt; signal &lt; 4,5V MIN:0x029, MAX:0x398 valid: 0..0x3FF, 0xFFFF signal invalid Internes Signal der JBBFE2 Not External JBBFE2 Input COM_MICRO PIN 19, PORT ADC6 |
| STAT_AUCSENSOR_EIN | int | AUC Sensor Eingang. Pin Wert. PWM Signale 0: NICHT AKTIV, 1: AKTIV (beständig) PIN 17, PORT P0.12 |
| STAT_PWM_PERIOD_AUCSENSOR_WERT | unsigned int | AUC Sensor Eingang Periode. Register wert Wertbereich: 0..0xFFFF(65535) PIN 17, PORT P0.12 |
| STAT_PERIOD_AUCSENSOR_WERT | real | AUC Sensor Eingang Periode. Physicalisher wert Wertbereich: 0..0xFFFF(65535) 0..131 ms 20 ms (50 Hz PWM): NORMAL [PERIOD]=(20ms/10000)*(STAT_PWM_PERIOD_AUCSENSOR_WERT) PIN 17, PORT P0.12 |
| STAT_PERIOD_AUCSENSOR_EINH | string | Einheit fuer AUC Sensor Eingang Periode: [Msek] |
| STAT_PWM_DUTY_AUCSENSOR_WERT | unsigned int | AUC Sensor Eingang Tastverhältnis (Duty). Register wert AUC Sensor Input Duty-Cycle. Register value Wertbereich: 0..0xFFFF(65535) 0.......:Kurzschluß nach Masse (SHORT-GND) 0xFFFF..:Leitungsunterbrechung (OPEN-LOAD) STAT_PWM_DUTY_AUCSENSOR_WERT &lt;= STAT_PWM_PERIOD_AUCSENSOR_WERT PIN 17, PORT P0.12 |
| STAT_DUTY_AUCSENSOR_WERT | real | AUC Sensor Eingang Tastverhältnis (Duty). Physicalisher wert AUC Sensor Input Duty-Cycle. Physical value Wertbereich: 0..0xFFFF(65535) 0..100 % [Duty]=(STAT_PWM_DUTY_AUCSENSOR_WERT*100)/(STAT_PWM_PERIOD_AUCSENSOR_WERT) PIN 17, PORT P0.12 |
| STAT_DUTY_AUCSENSOR_EINH | string | Einheit fuer AUC Sensor Eingang Tastverhältnis: [%] |
| STAT_T_ON_AUCSENSOR_WERT | real | AUC Sensor Eingang EIN Zeit Wertbereich: 0..0xFFFF(65535) 0..131 ms [T_ON]=(20ms/10000)*(STAT_PWM_DUTY_AUCSENSOR_WERT) PIN 17, PORT P0.12 |
| STAT_T_ON_AUCSENSOR_EINH | string | Einheit fuer AUC Sensor Eingang EIN Zeit: [Msek] |
| STAT_SITZHEIZUNG_FA_DIAG_EIN | int | Sitzheizung Fahrer Diagnose.Pin Wert. PWM Signale (25Hz) Seat Heating Driver Diagnosis 0: NICHT AKTIV, 1: AKTIV PIN 30, PORT P1.7 |
| STAT_SITZHEIZUNG_BF_DIAG_EIN | int | Sitzheizung Beifahrer Diagnose.Pin Wert. PWM Signale (25Hz) Seat Heating Passenger Diagnosis 0: NICHT AKTIV, 1: AKTIV PIN 19, PORT P0.14 |
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
| STAT_KOMPRESSORVENTIL_EIN | int | Kompressor-Ventil Ansteuerung. Pin Wert Compressor Valve Control. Pin value 0: AUS, 1: EIN 0: OFF, 1: ON PIN 39,PORT P2.0 |
| STAT_PWM_KOMPRESSORVENTIL_WERT | real | Spannung Kompressor-Ventil Ansteuerung PWM [V] Voltage Compressor Valve Control PWM Wertbereich: 0..0xFFFF (65535),Gültig:0..0x061B (1563)--&gt;0%..100% (PH)=(1563*Duty-cycle)/100, for Vref=5V PIN 39,PORT P2.0 |
| STAT_PWM_KOMPRESSORVENTIL_EINH | string | Einheit fuer PWM Kompressor-Ventil: Volt |
| STAT_PROZENT_KOMPRESSORVENTIL_WERT | int | Tastverhältnis Kompressor-Ventil Ansteuerung PWM [%] Duty-cycle Compressor Valve Control PWM [%] F = 400 Hz Wertbereich: 0%..100% PIN 39,PORT P2.0 |
| STAT_PROZENT_KOMPRESSORVENTIL_EINH | string | Einheit fuer Prozent Kompressor-Ventil : % |
| STAT_EVV_HS_EIN | int | PL4 (E70): electronische Volumenstrom-Ventil (EVV) High Side FET Ausgang. Pin Wert Servotronic (EVV) High Side FET Output. Pin value PL2-RED (E90_M3): EDC-Sport Switch Led 1 Indicator 0: AUS, 1: EIN 0: OFF, 1: ON PIN 43,PORT P2.4 |
| STAT_PWM_EVV_HS_WERT | int | electronische Volumenstrom-Ventil (EVV) High Side FET  PWM Ausgang Servotronic (EVV) High Side FET PWM Output Wertbereich: PIN 43,PORT P2.4 |
| STAT_PROZENT_EVV_HS_PWM_WERT | int | Tastverhältnis EVV_HS PWM Duty-Cycle EVV_HS PWM F = 400 Hz Wertbereich: 0%..100% PIN 43,PORT P2.4 |
| STAT_PROZENT_EVV_HS_PWM_EINH | string | Einheit fuer EVV-Ventils: % |
| STAT_SITZHEIZUNG_FA_EIN | int | Sitzheizung Fahrer Steuer Seat Heating Driver Control 0: LOW, 1: HIGH PIN 45,PORT P2.6 |
| STAT_PWM_SITZHEIZUNG_FA_WERT | int | Tastverhältnis Sitzheizung Fahrer PWM Duty-Cycle SeatHeating Driver Control F=25 Hz (fixed) (40 ms) 0: OFF (100% High Level. 40 ms ON), 1: STATE1 (80%. 32ms ON, 8ms OFF) 2: STATE2 (50%. 20ms ON, 20ms OFF), 3: STATE3 (30%. 12ms ON, 28ms OFF) PIN 45,PORT P2.6 |
| STAT_PWM_SITZHEIZUNG_FA_TEXT | string | Tastverhältnis Sitzheizung Fahrer PWM Duty-Cycle SeatHeating Driver Control OFF: 0 (100% High Level. 40 ms ON), STATE1: 1 (80%. 32ms ON, 8ms OFF) STATE2: 2 (50%. 20ms ON, 20ms OFF), STATE3: 3 (30%. 12ms ON, 28ms OFF) |
| STAT_SITZHEIZUNG_BF_EIN | int | Sitzheizung Beifahrer Steuer Seat Heating Passenger Control 0: LOW, 1: HIGH PIN 46,PORT P2.7 |
| STAT_PWM_SITZHEIZUNG_BF_WERT | int | Tastverhältnis Sitzheizung Beifahrer PWM Duty-Cycle SeatHeating Passenger Control F=25 Hz (fixed) (40 ms) 0: OFF (100% High Level. 40 ms ON), 1: STATE1 (80%. 32ms ON, 8ms OFF) 2: STATE2 (50%. 20ms ON, 20ms OFF), 3: STATE3 (30%. 12ms ON, 28ms OFF) PIN 46,PORT P2.7 |
| STAT_PWM_SITZHEIZUNG_BF_TEXT | string | Tastverhältnis Sitzheizung Beifahrer PWM Duty-Cycle SeatHeating Passenger Control OFF: 0 (100% High Level. 40 ms ON), STATE1: 1 (80%. 32ms ON, 8ms OFF) STATE2: 2 (50%. 20ms ON, 20ms OFF), STATE3: 3 (30%. 12ms ON, 28ms OFF) |
| STAT_EINH | string | Einheit fuer alle Analogausgangwerte: Volt |
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
| ORT | string | table DigitalInputNrTexte DINNR NAME |
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
| WERT2 | string | table AnalogInputNrTexte WERT nützlich nur fuer AUCSENSOR Tastverhältnis valid only for AUCSENSOR Duty-Cycle |
| ART_WERT | string | "nein"-&gt; ADC register Wert "ja"  -&gt; (PH) Wert default "nein" table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANALOG_INPUT_STATUS | string | ANALOG_INPUT_SET or ERROR_IN_ADDR or ERROR_IN_VALUE |
| ANALOG_INPUT_ADDR | string | ort |
| ANALOG_INPUT_VALUE | string | wert |
| ANALOG_INPUT_CONVERTED_VALUE | string | wert from JBBE (ADC oder (PH)) |
| ANALOG_INPUT_ART_WERT | string | art wert: ADC-Wert: 0 Physischeswert (PH): 1 |
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

<a id="job-steuern-beenden"></a>
### STEUERN_BEENDEN

Kontrolle an JBBFE zurueckgeben KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $02 Digitale Output $03 Analoge Input $04 Analoge Output $00 ReturnControToECU

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
| _TEL_ANTWORT1 | binary | Hex-Antwort1 von SG Digitale Input |
| _TEL_ANTWORT2 | binary | Hex-Antwort2 von SG Digitale Output |
| _TEL_ANTWORT3 | binary | Hex-Antwort3 von SG Analoge Input |
| _TEL_ANTWORT4 | binary | Hex-Antwort4 von SG Analoge Output |

<a id="job-status-var-iap-wws-ascet-input"></a>
### _STATUS_VAR_IAP_WWS_ASCET_INPUT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $00 Wiper/Washer System Ascet Model $00 Input Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MSGL_IN_KL50 | int |  |
| MSGL_IN_KLR | int |  |
| MSGL_KL58g | int |  |
| MSGL_IN_RSK_Front | int |  |
| MSGL_IN_RSK_Heck | int |  |
| MSGL_Niedr_Waschwasserstand | int |  |
| MSGL_Rgang | int |  |
| MSGL_Blocking_FrontWischer | int |  |
| MSGL_Blocking_HeckWischer | int |  |
| MSGL_Frontwaschen | int |  |
| MSGL_Heckwaschen | int |  |
| MSGL_Wischerschalter_Heckwischen | int |  |
| MSGL_Wisch_bei_Wasch_Heck | int |  |
| MSGL_Wisch_bei_Wasch | int |  |
| MSGL_RS_ImmediateChangeWiping | int |  |
| MSGL_RS_Notlauf | int |  |
| MSGL_RS_StartStop | int |  |
| MSGL_SZL_Notbetrieb | int |  |
| MSGL_Status_FrontWaschPumpe | int |  |
| MSGL_Status_FrontWischer | int |  |
| MSGL_Status_HeckWaschPumpe | int |  |
| MSGL_Status_HeckWischer | int |  |
| MSGL_Status_SRAWaschPumpe | int |  |
| MSGU_FZG_Geschwindigkeit | unsigned int |  |
| MSGU_GeschwKlasse | int |  |
| MSGU_IN_WISCHERSCHALTERHEBEL | int |  |
| MSGU_RS_WiperSpeed | int |  |
| MSGU_Wischerpoti | int |  |
| MSGE_WischFront_Out | int |  |
| MSGE_Scheibenwischerschalter | int |  |
| ascIN_StatusFeTraWe | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-wws-ascet-output"></a>
### _STATUS_VAR_IAP_WWS_ASCET_OUTPUT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $00 Wiper/Washer System Ascet Model $01 Output Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ascOUT_ST_Wisch_Front | int |  |
| ascOUT_ST_Wisch_FrontOut | int |  |
| ascOUT_ST_WischHeckOut | int |  |
| ascOUT_ST_WaschenFront | int |  |
| ascOUT_ST_WaschenHeck | int |  |
| ascOUT_ST_SRA | int |  |
| ascOUT_StartStopSRA | int |  |
| ascOUT_StartStopWiper_Back | int |  |
| ascOUT_StartStopWasch_Back | int |  |
| ascOUT_StartStopWasch_Front | int |  |
| ascOUT_FrontWiper_ImmediateChangeWiping | int |  |
| ascOUT_FrontWiper_Speed | int |  |
| ascOUT_WiperBack_ImmediatStop | int |  |
| dT | unsigned int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-wws-ascet-cod"></a>
### _STATUS_VAR_IAP_WWS_ASCET_COD

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $00 Wiper/Washer System Ascet Model $02 Coding Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PC_COD_DAUER_SPRITZIMPULS | unsigned int |  |
| PC_COD_PAUSE_ZW_SPRITZIMPULSE | unsigned int |  |
| PC_COD_SPERRZ_N_BLOCK_WI_FRONT | unsigned int |  |
| PC_COD_SPERRZ_N_BLOCK_WI_HECK | unsigned int |  |
| PC_COD_SRA_SPERRZEIT | unsigned int |  |
| PC_COD_WISCH_ERST_XXS_WASCH_FRONT | unsigned int |  |
| PC_COD_WISCH_ERST_XXS_WASCH_HECK | unsigned int |  |
| PL_COD_HECKSCHEIBE_VERBAUT | int |  |
| PL_COD_HECKWISCHEN_EIN_FRONTWISCHEN | int |  |
| PL_COD_HECKWISCHEN_EIN_RUECKWGANG | int |  |
| PL_COD_HECKWI_NACH_STOP_KLR_EIN | int |  |
| PL_COD_REGENSENSOR | int |  |
| PL_COD_RUECKSCHALTUNG_HS | int |  |
| PL_COD_SCHEIBENWA_BEI_WASSER_NIEDR | int |  |
| PL_COD_SCHEINWERFERREINIGUNG | int |  |
| PL_COD_SERVICEPOSITION | int |  |
| PL_COD_STANDRUECKSCHALTUNG | int |  |
| PL_COD_TAKTWASCHEN_HECK | int |  |
| PL_COD_ZYKLUS_VOLLENDEN_KLR_AUS | int |  |
| PU_COD_ANZAHL_NACHWISCHZ_FRONT | int |  |
| PU_COD_ANZAHL_NACHWISCHZ_HECK | int |  |
| PU_COD_ANZAHL_SPRITZIMPULSE | int |  |
| PU_COD_ANZAHL_WASCHBET_ZUR_SRA | int |  |
| PU_COD_ANZ_EIN_N_BLOCK_WI_FRONT | int |  |
| PU_COD_ANZ_EIN_N_BLOCK_WI_HECK | int |  |
| PU_COD_BLOCKERKENNUNG_WISCH_FRONT | int |  |
| PU_COD_BLOCKERKENNUNG_WISCH_HECK | int |  |
| PU_COD_INTERVALL_HECKWISCHER | int |  |
| PU_COD_WISCHERINTERVALL_STILL | int |  |
| PL_COD_WASCH_INAKTIV_HK_AUF | int |  |
| PL_COD_WASCH_INAKTIV_HS_AUF | int |  |
| PL_COD_WISCH_INAKTIV_HK_AUF | int |  |
| PL_COD_WISCH_INAKTIV_HS_AUF | int |  |
| PL_COD_WIWA_AKTIV_AB_KL15 | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-ascet-input"></a>
### _STATUS_VAR_IAP_PWR_ASCET_INPUT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $01 Power Window Ascet Model $00 Input Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ascIN_AutomaticBFTH | int |  |
| ascIN_AutomaticFATH | int |  |
| ascIN_DirectionBFTH | int |  |
| ascIN_DirectionFATH | int |  |
| ascIN_DriveBFTH | int |  |
| ascIN_DriveFATH | int |  |
| ascIN_DriveAckBFTH | int |  |
| ascIN_DriveAckFATH | int |  |
| ascIN_CtrChisl | int |  |
| ascIN_NormedBFTH | int |  |
| ascIN_NormedFATH | int |  |
| ascIN_PositionBFTH | int |  |
| ascIN_PositionFATH | int |  |
| ascIN_ReverseBFTH | int |  |
| ascIN_ReverseFATH | int |  |
| ascIN_StKl50 | int |  |
| ascIN_StPanMod | int |  |
| ascIN_StWrgEnb | int |  |
| ascIN_StartInitlaufBFTH | int |  |
| ascIN_StartInitlaufFATH | int |  |
| ascIN_Thermo90BFTH | int |  |
| ascIN_Thermo90FATH | int |  |
| ascIN_TraModus | int |  |
| ascIN_TuerOffenBFTH | int |  |
| ascIN_TuerOffenFATH | int |  |
| ascOP_LtAufBFTH | int |  |
| ascOP_LtAufFATH | int |  |
| ascOP_LtAutoBFTH | int |  |
| ascOP_LtAutoFATH | int |  |
| ascOP_LtZuBFTH | int |  |
| ascOP_LtZuFATH | int |  |
| ascOP_MstrAufBFTH | int |  |
| ascOP_MstrAufFATH | int |  |
| ascOP_MstrAutoBFTH | int |  |
| ascOP_MstrAutoFATH | int |  |
| ascOP_MstrZuBFTH | int |  |
| ascOP_MstrZuFATH | int |  |
| ascOP_SztAufBFTH | int |  |
| ascOP_SztAufFATH | int |  |
| ascOP_SztAutoBFTH | int |  |
| ascOP_SztAutoFATH | int |  |
| ascOP_SztZuBFTH | int |  |
| ascOP_SztZuFATH | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-ascet-output"></a>
### _STATUS_VAR_IAP_PWR_ASCET_OUTPUT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $01 Power Window Ascet Model $01 Output Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ascOUT_DenormBFTH | int |  |
| ascOUT_DenormFATH | int |  |
| ascOUT_DriveBFTH | int |  |
| ascOUT_DriveFATH | int |  |
| ascOUT_EksBFTH | int |  |
| ascOUT_EksFATH | int |  |
| ascOUT_InitResultBFTH | int |  |
| ascOUT_InitResultFATH | int |  |
| ascOUT_InitlaufBFTH | int |  |
| ascOUT_InitlaufFATH | int |  |
| ascOUT_PanicBFTH | int |  |
| ascOUT_PanicFATH | int |  |
| ascOUT_TargetPosBFTH | int |  |
| ascOUT_TargetPosFATH | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-ascet-cod"></a>
### _STATUS_VAR_IAP_PWR_ASCET_COD

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $01 Power Window Ascet Model $02 Coding Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ascCOD_FHTippAufBFTH | int |  |
| ascCOD_FHTippAufFATH | int |  |
| ascCOD_FHTippZuBFTH | int |  |
| ascCOD_FHTippZuFATH | int |  |
| ascCOD_FHMitEks | int |  |
| ascCOD_ManMitEks | int |  |
| ascCOD_Panikmodus | int |  |
| ascCOD_PanikmodusEks | int |  |
| ascCOD_TueraufStopMaut | int |  |
| ascCOD_Kl50Restart | int |  |
| ascCOD_WaitStWrgEnb | int |  |
| ascCOD_TimeWaitStWrgEnb | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-pwr"></a>
### _STATUS_VAR_CAN_PWR

Auslesen der Stati von den Fensterheber CAN Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 CAN Variables $01 ReportCurrentState $08 PWR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PWEnable | int |  |
| PWPanicMode | int |  |
| PWChildSafety | int |  |
| PWRearDrvComfortCommand | int |  |
| PWRearPsgComfortCommand | int |  |
| PWDrvRearDrvSwitch | int |  |
| PWDrvRearPsgSwitch | int |  |
| PWRearDrvSwitch | int |  |
| PWRearPsgSwitch | int |  |
| PWPsgSwitch | int |  |
| PWRearDrvPosition_Pulses | int |  |
| PWRearPsgPosition_Pulses | int |  |
| PWRearDrvPosition_Mm | int |  |
| PWRearPsgPosition_Mm | int |  |
| PWRearDrvPosition_Status | int |  |
| PWRearPsgPosition_Status | int |  |
| PWRearDrvDrivingDirection | int |  |
| PWRearPsgDrivingDirection | int |  |
| PWRearDrvErrorStatus | int |  |
| PWRearPsgErrorStatus | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr"></a>
### _STATUS_VAR_IAP_PWR

Auslesen der Stati von den Fnesterheber Internal Varablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $08 PWR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PWDelayElmos | int |  |
| PWReqBlock | int |  |
| PWRearDrvHall1Defect | int |  |
| PWRearPsgHall1Defect | int |  |
| PWRearDrvHall2Defect | int |  |
| PWRearPsgHall2Defect | int |  |
| PWRearDrvRelay1Defect | int |  |
| PWRearPsgRelay1Defect | int |  |
| PWRearDrvRelay2Defect | int |  |
| PWRearPsgRelay2Defect | int |  |
| PWSend_RearDrvPOSITION | int |  |
| PWSend_RearPsgPOSITION | int |  |
| ST_Hall_Sensor_PW_DrvClose | int |  |
| ST_Hall_Sensor_PW_DrvOpen | int |  |
| ST_Hall_Sensor_PW_PsgClose | int |  |
| ST_Hall_Sensor_PW_PsgOpen | int |  |
| ST_PW_DrvClose | int |  |
| ST_PW_DrvOpen | int |  |
| ST_PW_PsgClose | int |  |
| ST_PW_PsgOpen | int |  |
| Status_CTR_FH_FAT_msg | int |  |
| Status_CTR_FH_SHD_ZENTRALE_msg | int |  |
| PWR_CCM_Denorm_Panic | int |  |
| PWR_CCM_HwDefect | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-fzm"></a>
### _STATUS_VAR_IAP_FZM

Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $09 FZM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FzmWakeupReason | int |  |
| FzmActivateWakeupECU | int |  |
| WakeUpReason | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-atmel"></a>
### _STATUS_VAR_IAP_ATMEL

Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables $01 ReportCurrentState $0A Atmel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| WakeUpReason | int |  |
| slm_T_Diag_Delay | int |  |
| AtmelWakeUpIndication | int |  |
| AtmelPreSleepIndication | int |  |
| WakeUpInputsState | int |  |
| CAN_ID | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-comicro"></a>
### _FLASH_COMICRO

Internen Flashvorgang des Co-Prozessors anstossen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE4 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-comicro"></a>
### _STATUS_COMICRO

KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C200 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_COMICRO_VERSION | int | The comicro version number |
| STAT_PORT_B | int | Status of comicro port B |
| STAT_PORT_C | int | Status of comicro port C |
| STAT_PORT_D | int | Status of comicro port D |
| STAT_SLEEP | int | Status of comicro port D |
| STAT_COMICRO | int | Status of comicro port D |

<a id="job-lear-plx-eol-configuration"></a>
### _LEAR_PLx_EOL_CONFIGURATION

Configuration for the LEAR End of Line KWP2000: $3B WriteDataByLocalIdentifier $7A RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VARIANT_BYTE | string | Variant table Variant_table VARIANT_BYTE |
| SERIENNUMMER | string | serial number 9-stellig |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TTMMJJ |
| AIF_ZB_NR | string | Zusammenbaunummer 7-stellig |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-read-variant"></a>
### READ_VARIANT

Lesen der Variante der Plattine KWP2000: $21 ReadDataByLocalIdentifier $6E RecordLocalId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VARIANT | string | Variant table Variant_table-&gt;VARIANT_BYTE |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-waschduese-aussenspiegel"></a>
### STEUERN_WASCHDUESE_AUSSENSPIEGEL

Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $79 RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_JWH_TIMER | unsigned int | Control the Jet Washer and Mirror Heater for the time passed in this parameter. Unit: Steps of 10 ms (milliseconds) Steuern der Waschduesen/Aussenspiegelheizung während die in diesem Parameter eingefuehrte Zeit Einheit: Stufen von 10 ms (MILLISEKUNDEN) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-eeprom-init"></a>
### _EEPROM_INIT

Initialise the EEPROM KWP2000: $3B WriteDataByLocalIdentifier $7E RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACTION | string | Action to do with the EEPROM table Eeprom_Init_table ACTION_BYTE |

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

<a id="job-dtc-enable-get"></a>
### _DTC_ENABLE_GET

KWP2000: $21 ReadDataByLocalIdentifier $70 RecordLocalId Returns the status of DTC_enable Cache14 2 bit / DTC 1st ..... Enabled/ Disabled 2nd ..... Protect / Unprotect Load

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DTC_00 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_01 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_02 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_03 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_04 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_05 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_06 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_07 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_08 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_09 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_10 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_11 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_12 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_13 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_14 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_15 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_16 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_17 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DTC_18 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dtc-enable-set"></a>
### _DTC_ENABLE_SET

Modifies EEpromCache14 (DTC enable/disable) KWP2000: $3B WriteDataByLocalIdentifier $70 RecordLocalId 2 bit / DTC 1st ..... Enabled/ Disabled 2nd ..... Protect / Unprotect Load

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Byte-number where the DTC is included |
| WERT | string | Value to be stored |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dtc-enable-all"></a>
### _DTC_ENABLE_ALL

Modifies EEpromCache14 (DTC enable/disable) KWP2000: $3B WriteDataByLocalIdentifier $71 RecordLocalId Sets all DTCs for Protection

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dtc-disable-all"></a>
### _DTC_DISABLE_ALL

Modifies EEpromCache14 (DTC enable/disable) KWP2000: $3B WriteDataByLocalIdentifier $72 RecordLocalId Sets all DTCs for Protection

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schalterblock-tuer"></a>
### STATUS_SCHALTERBLOCK_TUER

Abfragen der Stati der angeschlossenen Schalterbloecke KWP2000: $30 InputOutputControlByLocalIdentifier $08 BAUSTEIN_TUER $01 ReportCurrentState $00 SCHALTERBLOCK_TUER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FH_TASTERBF_BF_ZU | int | Beifahrerseite (lokaler Taster) Fensterheber Beifahrerseite zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERBF_BF_AUF | int | Beifahrerseite (lokaler Taster) Fensterheber Beifahrerseite auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERBF_BF_MAUT_ZU | int | Beifahrerseite (lokaler Taster) Fensterheber Beifahrerseite Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERBF_BF_MAUT_AUF | int | Beifahrerseite (lokaler Taster) Fensterheber Beifahrerseite Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERBF_BF_WERT | int | Beifahrerseite (lokaler Taster) Fensterheber Beifahrerseite 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTERFA_FAH_ZU | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite hinten zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FAH_AUF | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite hinten auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FAH_MAUT_ZU | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite hinten Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FAH_MAUT_AUF | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite hinten Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FAH_WERT | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite hinten 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTERFAH_FAH_ZU | int | Fahrerseite hinten (lokaler Taster) Fensterheber Fahrerseite hinten zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFAH_FAH_AUF | int | Fahrerseite hinten (lokaler Taster) Fensterheber Fahrerseite hinten auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFAH_FAH_MAUT_ZU | int | Fahrerseite hinten (lokaler Taster) Fensterheber Fahrerseite hinten Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFAH_FAH_MAUT_AUF | int | Fahrerseite hinten (lokaler Taster) Fensterheber Fahrerseite hinten Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFAH_FAH_WERT | int | Fahrerseite hinten (lokaler Taster) Fensterheber Fahrerseite hinten 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTERFA_BFH_ZU | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BFH_AUF | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BFH_MAUT_ZU | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BFH_MAUT_AUF | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BFH_WERT | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTEBFH_BFH_ZU | int | Beifahrerseite hinten (lokaler Taster) Fensterheber Beifahrerseite hinten zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERBFH_BFH_AUF | int | Beifahrerseite hinten (lokaler Taster) Fensterheber Beifahrerseite hinten auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERBFH_BFH_MAUT_ZU | int | Beifahrerseite hinten (lokaler Taster) Fensterheber Beifahrerseite hinten Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERBFH_BFH_MAUT_AUF | int | Beifahrerseite hinten (lokaler Taster) Fensterheber Beifahrerseite hinten Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERBFH_BFH_WERT | int | Beifahrerseite hinten (lokaler Taster) Fensterheber Beifahrerseite hinten 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_ROLLO_HECK_TASTER_EIN | int | 0: Taster Heckrollo nicht gedrueckt 1: Taster Heckrollo gedrueckt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tuer"></a>
### STATUS_TUER

Status-Abfragen Tuer Beinhaltet Fenster, Fensterheber, Spiegel und Zentralverriegelung KWP2000: $30 InputOutputControlByLocalIdentifier $08 BAUSTEIN_TUER $01 ReportCurrentState $01 STATUS_TUER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UBATT_WERT | real | (Klemme 30) Spannung am Steuergeraet in Volt Aufloesung 0,028 V/Bit |
| STAT_UBATT_EINH | string | (Klemme 30) Spannung am Steuergeraet in Volt Aufloesung 0,028 V/Bit |
| STAT_UBATT_LOW | int | 0: Keine Unterspannung detektiert 1: Unterspannung (&lt;12V) an Klemme 30 detektiert (min. Spannung für das Einlernen der Fenster) |
| STAT_UBATT_OVR | int | 0: Keine Ueberspannung detektiert 1: Ueberspannung (&gt;16V) an Klemme 30 detektiert |
| STAT_FH_FAH_OFFEN_KOMPLETT | int | Fenster Fahrerseite hinten komplett offen 0: geschlossen oder halb offen 1: komplett offen |
| STAT_FH_FAH_GESCHLOSSEN_KOMPLETT | int | Fenster Fahrerseite hinten komplett geschlossen 0: offen oder halb geschlossen 1: komplett geschlossen |
| STAT_FH_FAH_FAEHRT_AUF | int | 0: - 1: Fensterheber Fahrerseite hinten faehrt auf |
| STAT_FH_FAH_FAEHRT_ZU | int | 0: - 1: Fensterheber Fahrerseite hinten faehrt zu |
| STAT_FH_FAH_EINLERNENVORGANG_AKTIV | int | 0: Einlernvorgang (Fensterheber Fahrerseite hinten) nicht aktiv 1: Einlernvorgang (Fensterheber Fahrerseite hinten) aktiv |
| STAT_FH_FAH_EINGELERNT | int | 0: Fensterheber Fahrerseite hinten nicht eingelernt 1: Fensterheber Fahrerseite hinten eingelernt |
| STAT_FH_FAH_POSITION_WERT | int | Position Fensterheber Fahrerseite hinten, nur bei eingelerntem FH 0: Fenster ungueltiger Zustand 1: Fenster im gueltigen Zustand (max. Wert bei Fenster geschlossen) Wertbereich: PL4:     0-550 mm PL2-RED: 0-450 mm |
| STAT_FH_FAH_POSITION_EINH | string | Einheit Position Fensterheber Fahrerseite hinten |
| STAT_FH_BFH_OFFEN_KOMPLETT | int | Fenster Beifahrerseite hinten komplett offen 0: geschlossen oder halb offen 1: komplett offen |
| STAT_FH_BFH_GESCHLOSSEN_KOMPLETT | int | Fenster Beifahrerseite hinten komplett geschlossen 0: offen oder halb geschlossen 1: komplett geschlossen |
| STAT_FH_BFH_FAEHRT_AUF | int | 0: - 1: Fensterheber Beifahrerseite hinten faehrt auf |
| STAT_FH_BFH_FAEHRT_ZU | int | 0: - 1: Fensterheber Beifahrerseite hinten faehrt zu |
| STAT_FH_BFH_EINLERNENVORGANG_AKTIV | int | 0: Einlernvorgang (Fensterheber Beifahrerseite hinten) nicht aktiv 1: Einlernvorgang (Fensterheber Beifahrerseite hinten) aktiv |
| STAT_FH_BFH_EINGELERNT | int | 0: Fensterheber Beifahrerseite hinten nicht eingelernt 1: Fensterheber Beifahrerseite hinten eingelernt |
| STAT_FH_BFH_POSITION_WERT | int | Position Fensterheber Beifahrerseite hinten, nur bei eingelerntem FH 0: Fenster ungueltiger Zustand 1: Fenster im gueltigen Zustand (max. Wert bei Fenster geschlossen) Wertbereich: PL4:     0-550 mm PL2-RED: 0-450 mm |
| STAT_FH_BFH_POSITION_EINH | string | Einheit Position Fensterheber Beifahrerseite hinten |
| STAT_SPIEGEL_HEIZUNG_EIN | int | 0: Spiegelheizung ausgeschaltet 1: Spiegelheizung eingeschaltet |
| STAT_SPIEGEL_HEIZUNG_WERT | int | Aktueller Wert der Spiegelheizung |
| STAT_SPIEGEL_HEIZUNG_EINH | string | % |
| STAT_SPIEGEL_HEIZUNG_MOEGLICH | int | 0: Spiegel kann nicht beheizt werden 1: Spiegel kann beheizt werden |
| STAT_ZV_FA_ENTRIEGELT | int | 0: - 1: Zentralverriegelung Fahrerseite entriegelt |
| STAT_ZV_BF_ENTRIEGELT | int | 0: - 1: Zentralverriegelung Beifahrerseite entriegelt |
| STAT_ZV_FAH_ENTRIEGELT | int | 0: - 1: Zentralverriegelung Fahrerseite hinten entriegelt |
| STAT_ZV_BFH_ENTRIEGELT | int | 0: - 1: Zentralverriegelung Beifahrerseite hinten entriegelt |
| STAT_ZV_FA_VERRIEGELT | int | 0: - 1: Zentralverriegelung Fahrerseite verriegelt |
| STAT_ZV_BF_VERRIEGELT | int | 0: - 1: Zentralverriegelung Beifahrerseite verriegelt |
| STAT_ZV_FAH_VERRIEGELT | int | 0: - 1: Zentralverriegelung Fahrerseite hinten verriegelt |
| STAT_ZV_BFH_VERRIEGELT | int | 0: - 1: Zentralverriegelung Beifahrerseite hinten verriegelt |
| STAT_KISI_FH_FAH_AKTIV | int | 0: Kindersicherung Fensterheber und Sonnenrollo Fahrer hinten sind nicht gesperrt 1: Kindersicherung Fensterheber und Sonnenrollo Fahrer hinten sind gesperrt. D.h. sie können nur vom Fahrer aus gesteuert werden |
| STAT_KISI_FH_BFH_AKTIV | int | 0: Kindersicherung Fensterheber und Sonnenrollo Beifahrer hinten sind nicht gesperrt 1: Kindersicherung Fensterheber und Sonnenrollo Beifahrer hinten sind gesperrt. D.h. sie können nur vom Fahrer aus gesteuert werden |
| STAT_ROLLO_HECK_BLOCK | int | Heckscheibe Sonnenrollo Heckscheibe komplett ausgefahren 0: Endposition nicht erreicht 1: Endposition erreicht |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-tuer"></a>
### STEUERN_DIGITAL_TUER

Ansteuerung der digitalen Eingaenge KWP2000: $30 InputOutputControlByLocalIdentifier $08 BAUSTEIN_TUER $07 ShortTermAdjustment $02 STEUERN_TUER

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | int | Auswahl des Elements (ARGUMENT aus table STEUERN_DIGITAL_VERFAHREN) |
| AKTION | int | Aktion die durchgefuehrt werden soll Bei digitalen Ansteuerungen entweder 0 oder 1 Bei Ansteuerungen per Zeitangabe wird die Zeit in ms-Schritten angegeben Max.7000 (7 sek.) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegel-heizung"></a>
### STEUERN_SPIEGEL_HEIZUNG

Ein bzw. Ausschalten der Spiegelheizung per Diagnose

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGEL_HEIZUNG | int | 0: Spiegelheizung ausschalten 1: Spiegelheizung einschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zwp"></a>
### STEUERN_ZWP

Schreiben die Zussatzwasserpumpe parameter KWP2000: $3B WriteDataByLocalIdentifier $77 RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_ZWP_TIMER | unsigned int | Control the Additional water pump for the time passed in this parameter. Unit: Steps of 10 ms (milliseconds) Steuern der Zussatzwasserpumpen während die in diesem Parameter eingefuehrte Zeit Einheit: Stufen von 10 ms (MILLISEKUNDEN) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wasserventil-fahrer"></a>
### STEUERN_WASSERVENTIL_FAHRER

Schreiben die Wasserventil parameter KWP2000: $3B WriteDataByLocalIdentifier $78 RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_WV_TIMER | unsigned int | Control the  water valve 1 (fahrer)  for the time passed in this parameter. Unit: Steps of 10 ms (milliseconds) Steuern der wasserventil während die in diesem Parameter eingefuehrte Zeit Einheit: Stufen von 10 ms (MILLISEKUNDEN) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wasserventil-beifahrer"></a>
### STEUERN_WASSERVENTIL_BEIFAHRER

Schreiben die Wasserventil parameter KWP2000: $3B WriteDataByLocalIdentifier $76 RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_WV_TIMER | unsigned int | Control the  water valve 2 (beifahrer) for the time passed in this parameter. Unit: Steps of 10 ms (milliseconds) Steuern der wasserventil während die in diesem Parameter eingefuehrte Zeit Einheit: Stufen von 10 ms (MILLISEKUNDEN) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierbits"></a>
### STATUS_CODIERBITS

Einige Codierdaten lesen KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REGENSENSOR_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_WASCHDUESEN_HEIZUNG_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_SPIEGELHEIZUNG_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_SRA_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_HECKSCHEIBEN_TASTER_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_DSC_TASTER_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_ZUSATZWASSERPUMPE_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_KOMPRESSORVENTIL_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_KOMPRESSORVENTIL_MIN_STROM_WERT | real | KOMPRESSOR STROM BEI 1% PULSEVERHAELTNIS [AMPERES] |
| STAT_KOMPRESSORVENTIL_MAX_STROM_WERT | real | KOMPRESSOR STROM BEI 100% PULSEVERHAELTNIS [AMPERES] |
| STAT_WASSERVENTIL_1_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_WASSERVENTIL_2_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_AUC_SENSOR_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_DRUCKSENSOR_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_FONDSCHICHTUNGS_POTI_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_STANDHEIZUNG_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_SITZHEIZUNG_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_SITZHEIZUNG_NACHLAUFZEIT_WERT | int | [MINUTEN] 255: ungueltiger Wert |
| STAT_SONNENROLLO_HECK_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_HANDSCHUHFACH_TASTER_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_LADERAUMABDECKUNG_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_FENSTERHEBER_HINTEN_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_FENSTERHEBER_HINTEN_EKS_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_FENSTERHEBER_HINTEN_TUERAUF_STOP_MAUT_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_FENSTERHEBER_HINTEN_THERMOSCHUTZ_WERT | int | [GRAD CELSIUS] |
| STAT_BISTABILES_RELAIS_VORNE_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_BISTABILES_RELAIS_HINTEN_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_HECKWISCHER_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_KOMPRESSOR_MAGNET_KUPPLUNG_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_DRITTE_SITZREIHE_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_EDC_TASTER_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| STAT_SCA_HECKKLAPPE_COD_EIN | int | 0: NICHT AKTIV, 1: AKTIV |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG_BLOCK_0 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_BLOCK_0 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_BLOCK_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_BLOCK_3 | binary | Hex-Antwort von SG |

<a id="job-save-lear-eol-data"></a>
### _SAVE_LEAR_EOL_DATA

Data available for the LEAR End of Line KWP2000: $3B WriteDataByLocalIdentifier $7B RecordLocalId

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEAR_PART_NUMBER | string | Lear part number 9-digits |
| YEAR | string | Year 20xx 2-digits |
| DAY_OF_THE_YEAR | string | Day of the year 3-digits |
| SERIAL_NUMBER | string | Serial Number 3-digits |
| BOARD_IDENTIFIER | string | Board identifier 1-digit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-read-lear-eol-data"></a>
### _READ_LEAR_EOL_DATA

KWP 2000: $21   ReadDataByCommonIdentifier KWP 2000: $75   ProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LEAR_PART_NUMBER | string | Lear part number 9 digits |
| STAT_YEAR | string | Year |
| STAT_DAY_OF_THE_YEAR | string | The day of the year |
| STAT_SERIAL_NUMBER | string | Serial number (Base 34 and Rolling) |
| STAT_BOARD_IDENTIFIER | string | Board identifier A,B or C in a Panel |

<a id="job-performance-analysis"></a>
### _PERFORMANCE_ANALYSIS

Reading the Performing Analysis KWP2000: $21 ReadDataByLocalIdentifier $6C RecordLocalId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TASK_5 | unsigned int | time consumption in ms |
| TASK_10A | unsigned int | time consumption in ms |
| TASK_10B | unsigned int | time consumption in ms |
| TASK_20A | unsigned int | time consumption in ms |
| TASK_20B | unsigned int | time consumption in ms |
| TASK_20C | unsigned int | time consumption in ms |
| TASK_20D | unsigned int | time consumption in ms |
| TASK_40A | unsigned int | time consumption in ms |
| TASK_40C | unsigned int | time consumption in ms |
| TASK_80D | unsigned int | time consumption in ms |
| TASK_80F | unsigned int | time consumption in ms |
| SLICE | unsigned int | time consumption in ms |
| INTERRUPTS_COUNTER | unsigned int | How many interrupts |
| INTERRUPTS | unsigned int | time consumption in ms |
| MAX_CPU_LOAD | unsigned int | max cpu consumption in % |
| AVG_CPU_LOAD | unsigned int | avg cpu consumption in % |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (72 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (13 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (12 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (23 × 9)
- [TABLE_C801](#table-table-c801) (1 × 6)
- [TABLE_C802](#table-table-c802) (1 × 14)
- [TABLE_C803](#table-table-c803) (1 × 11)
- [TABLE_C804](#table-table-c804) (1 × 6)
- [TABLE_C805](#table-table-c805) (1 × 14)
- [TABLE_C806](#table-table-c806) (1 × 11)
- [TABLE07_08_09_0A_0C](#table-table07-08-09-0a-0c) (1 × 5)
- [TABLE_C80B](#table-table-c80b) (1 × 9)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [EEPROM_INIT_TABLE](#table-eeprom-init-table) (4 × 3)
- [VARIANT_TABLE](#table-variant-table) (3 × 3)
- [AUSWAHL_FENSTER](#table-auswahl-fenster) (6 × 2)
- [FH_RICHTUNG](#table-fh-richtung) (10 × 3)
- [FH_EINLERNEN](#table-fh-einlernen) (8 × 2)
- [FH_DENORM_FEHLERTEXTE](#table-fh-denorm-fehlertexte) (26 × 2)
- [FH_REVERSIER_FEHLERTEXTE](#table-fh-reversier-fehlertexte) (8 × 2)
- [FH_AUSWAHL_BAUREIHE](#table-fh-auswahl-baureihe) (2 × 3)
- [FUNKTIONALEADRESSE_LEAR](#table-funktionaleadresse-lear) (7 × 3)
- [DIGITALINPUTNRTEXTE](#table-digitalinputnrtexte) (33 × 4)
- [DIGITALOUTPUTNRTEXTE](#table-digitaloutputnrtexte) (35 × 4)
- [ANALOGINPUTNRTEXTE](#table-analoginputnrtexte) (28 × 4)
- [ANALOGOUTPUTNRTEXTE](#table-analogoutputnrtexte) (5 × 4)
- [STEUERN_DIGITAL_VERFAHREN](#table-steuern-digital-verfahren) (28 × 3)
- [ZUORDNUNG_CAN_ID_SG](#table-zuordnung-can-id-sg) (409 × 7)

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

Dimensions: 77 rows × 2 columns

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
| 0x76 | CEL |
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
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 72 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9C5E | DRUCK_SENSOR |
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
| 0xA6D2 | WASSERVENTIL_1 |
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
| 0xA6DD | SONNENROLLO_LADERAUMABDECKUNG |
| 0xA6DE | AUSSENSPIEGEL_HEIZUNG |
| 0xA6E0 | SITZHEIZUNG_FAHRER |
| 0xA6E1 | SITZHEIZUNG_BEIFAHRER |
| 0xA6E2 | SCA_RELAIS |
| 0xA6E3 | HECKKLAPPE_OBEN |
| 0xA6E4 | SENSOR_TANK_LINKS |
| 0xA6E5 | SENSOR_TANK_RECHTS |
| 0xA6E6 | SCHALTER_FH_BEIFAHRER_VORNE |
| 0xA6E7 | Energiesparmode aktiv |
| 0xA6E8 | ZV_WIEDERHOLSPERRE |
| 0xA6E9 | VERDECKKASTENSCHLOSS |
| 0xA728 | SCHALTER_FH_BEIFAHRER_HINTEN |
| 0xA729 | SCHALTER_FH_FAHRER_HINTEN |
| 0xA72A | HALLSENSOR1_FH_FA_HINTEN |
| 0xA72B | HALLSENSOR2_FH_FA_HINTEN |
| 0xA72C | HALLSENSOR1_FH_BF_HINTEN |
| 0xA72D | HALLSENSOR2_FH_BF_HINTEN |
| 0xA72E | WASSERVENTIL_2 |
| 0xA72F | KOMPRESSOR_KUPPLUNG |
| 0xA730 | BISTABILES_RELAIS_1 |
| 0xA731 | BISTABILES_RELAIS_2 |
| 0xA732 | PT_WAKEUP_LEITUNG |
| 0xA733 | DC_DC_WANDLER |
| 0xA734 | EVV_VENTIL_ABSCHALTURSACHE |
| 0xA735 | EVV_VENTIL_ANSTEURPFAD_1 |
| 0xA736 | EVV_VENTIL_ANSTEURPFAD_2 |
| 0xA737 | K_CAN_ID2BF_PL4_WASSERVENTIL_TIMEOUT |
| 0xC907 | K_CAN_KOMMUNIKATION |
| 0xC908 | K_CAN_EINTRAHT_BETRIEB |
| 0xC90B | PT_CAN_KOMMUNIKATION |
| 0xC914 | K_CAN_ID246_STATUSKLIMA_TIMEOUT |
| 0xC915 | K_CAN_ID246_KOMPRESSORVENTIL_UNGUELT |
| 0xC916 | K_CAN_ID246_HECKSCHHEIZUNG_UNGUELT |
| 0xC917 | K_CAN_ID246_ZUSWASSERPUMP_UNGUELT |
| 0xC918 | PT_CAN_ID2A6_BEDIENUNG_WISCHER_TIMEOUT |
| 0xC919 | PT_CAN_ID1B6_TIMEOUT |
| 0xC91A | PT_CAN_ID1B6_WASSERV_UNGUELT |
| 0xC91B | K_CAN_ID1E7_SITZHEIZUNG_FA_UNGUELT |
| 0xC91C | K_CAN_ID1E8_SITZHEIZUNG_BF_UNGUELT |
| 0xC91D | K_CAN_ID246_KOMPRESSOR_KUPPLUNG_UNGUELT |
| 0xC91E | K_CAN_ID_130_KLEMMENSTATUS |
| 0xC91F | K_CAN_ID_330_KILOMETERSTAND_REICHWEITE_TIMEOUT |
| 0xC920 | PT_CAN_ID_1A0_GESCHWINDIGKEIT |
| 0xC921 | PT_CAN_ID_AA_TORQUE_3 |
| 0xC922 | PT_CAN_ID_C4_LENKRADWINKEL |
| 0xC923 | PT_CAN_ID_B5_DREHMOMENT_ANF_EGS_UNGUELT |
| 0xC924 | PT_CAN_ID_B5_DREHMOMENT_ANF_EGS_TIMEOUT |
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
| 0x01 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 10 | 0 |
| 0x02 | BatterieSpannung | volt | high | unsigned int | - | 6675 | 240640 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

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

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC801 | ERR_SWITCH_RESET_SVAUS |
| 0xC802 | ERR_SWITCH_RESET_WAKEUP |
| 0xC803 | ERR_SWITCH_RESET_NOT_SLEEP |
| 0xC804 | ERR_SWITCH_OFF_STROMZWEIG |
| 0xC805 | ERR_SWITCH_OFF_WAKEUP |
| 0xC806 | ERR_SWITCH_OFF_NOT_SLEEP |
| 0xC807 | ERR_SWITCH_OFF_TRANSPORT |
| 0xC808 | DIAG_PWRDWN_BEI_NICHT_EINSCHLAFEN |
| 0xC809 | DIAG_PWRDWN_BEI_WECKER |
| 0xC80A | DIAG_RESET_BEI_NICHT_EINSCHLAFEN |
| 0xC80B | DAUER_EIN_KL15_KLR |
| 0xC80C | ERR_DIAG_CAN_KOMMUNIKATION |
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
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 12 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xC801 | Table_C801 | - | - | - |
| 0xC802 | Table_C802 | - | - | - |
| 0xC803 | Table_C803 | - | - | - |
| 0xC804 | Table_C804 | - | - | - |
| 0xC805 | Table_C805 | - | - | - |
| 0xC806 | Table_C806 | - | - | - |
| 0xC807 | Table07_08_09_0A_0C | - | - | - |
| 0xC808 | Table07_08_09_0A_0C | - | - | - |
| 0xC809 | Table07_08_09_0A_0C | - | - | - |
| 0xC80A | Table07_08_09_0A_0C | - | - | - |
| 0xC80B | Table_C80B | - | - | - |
| 0xC80C | Table07_08_09_0A_0C | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 23 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x02 | AUSSEN_TEMP | Grad C | low | unsigned char | - | 0.5 | 1 | -40 |
| 0x03 | VBAT_WHEN_KL15 | Volt | low | unsigned int | - | 1335 | 48128 | 0 |
| 0x04 | CURRENT_VBAT | Volt | low | unsigned int | - | 1335 | 48128 | 0 |
| 0x06 | STAT_RELATIVZEIT_WERT | s | low | signed long | - | 1 | 1 | 0 |
| 0x07 | STAT_WECKER_CAN_ID_1 | Hex | low | unsigned int | - | 1 | 1 | 0 |
| 0x08 | STAT_WECKER_CAN_ID_1 | Hex | low | unsigned int | - | 1 | 1 | 0 |
| 0x09 | STAT_WECKER_CAN_ID_1 | Hex | low | unsigned int | - | 1 | 1 | 0 |
| 0x0A | STAT_WECKER_CAN_ID_1 | Hex | low | unsigned int | - | 1 | 1 | 0 |
| 0x0B | WECKER_CAN_ANZ_1 | 1-n | low | unsigned char | - | 1 | 1 | 0 |
| 0x0C | WECKER_CAN_ANZ_2 | 1-n | low | unsigned char | - | 1 | 1 | 0 |
| 0x0D | WECKER_CAN_ANZ_3 | 1-n | low | unsigned char | - | 1 | 1 | 0 |
| 0x0E | WECKER_CAN_ANZ_4 | 1-n | low | unsigned char | - | 1 | 1 | 0 |
| 0x0F | DELTA_T_TIMER | s | low | signed long | - | 1 | 1 | 0 |
| 0x11 | DURATION_TIMER | s | low | unsigned int | - | 1 | 1 | 0 |
| 0x12 | WAKE_LINE | 1/0 | low | unsigned char | - | 1 | 1 | 0 |
| 0x13 | STAT_VERURSACHER_1 | Hex | low | unsigned char | - | 1 | 1 | 0 |
| 0x14 | STAT_VERURSACHER_2 | Hex | low | unsigned char | - | 1 | 1 | 0 |
| 0x15 | STAT_VERURSACHER_3 | Hex | low | unsigned char | - | 1 | 1 | 0 |
| 0x16 | STAT_VERURSACHER_4 | Hex | low | unsigned char | - | 1 | 1 | 0 |
| 0x17 | BIT_FÜR_CC-MELDUNG | 1/0 | low | unsigned char | - | 1 | 1 | 0 |
| 0x18 | KL15_ANTEIL | 1-n | low | unsigned char | - | 1 | 1 | 0 |
| 0x19 | KL0_ANTEIL | 1-n | low | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-table-c801"></a>
### TABLE_C801

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x02 | 0x03 | 0x04 | 0x06 | 0x0F |

<a id="table-table-c802"></a>
### TABLE_C802

Dimensions: 1 rows × 14 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 13 | 0x02 | 0x03 | 0x04 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F |

<a id="table-table-c803"></a>
### TABLE_C803

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x02 | 0x03 | 0x04 | 0x06 | 0x13 | 0x14 | 0x15 | 0x16 | 0x11 | 0x12 |

<a id="table-table-c804"></a>
### TABLE_C804

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x02 | 0x03 | 0x04 | 0x06 | 0x0F |

<a id="table-table-c805"></a>
### TABLE_C805

Dimensions: 1 rows × 14 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 13 | 0x02 | 0x03 | 0x04 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F |

<a id="table-table-c806"></a>
### TABLE_C806

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x02 | 0x03 | 0x04 | 0x06 | 0x13 | 0x14 | 0x15 | 0x16 | 0x11 | 0x12 |

<a id="table-table07-08-09-0a-0c"></a>
### TABLE07_08_09_0A_0C

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x02 | 0x03 | 0x04 | 0x06 |

<a id="table-table-c80b"></a>
### TABLE_C80B

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x02 | 0x03 | 0x04 | 0x06 | 0x11 | 0x17 | 0x18 | 0x19 |

<a id="table-energysaving"></a>
### ENERGYSAVING

Dimensions: 5 rows × 3 columns

| E_MODE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | ENERGY_MODE_AUS | Kein Energiesparmode |
| 0x01 | ENERGY_MODE_PRODUCTION | Produktionsmode |
| 0x02 | ENERGY_MODE_SHIPMENT | Transportmode |
| 0x04 | ENERGY_MODE_REPAIR_SHOP | Werkstattmode |
| 0x08 | ERROR | falscher Eingabewert |

<a id="table-eeprom-init-table"></a>
### EEPROM_INIT_TABLE

Dimensions: 4 rows × 3 columns

| ACTION_NUMBER | ACTION_BYTE | ACTION_NAME |
| --- | --- | --- |
| 0x00 | CODING | default Codierung |
| 0x01 | DTC | Fehlerspeicher loeschen |
| 0x02 | ALL | EEPROM komplett loeschen |
| 0xXY | -- | -- |

<a id="table-variant-table"></a>
### VARIANT_TABLE

Dimensions: 3 rows × 3 columns

| VARIANT_NUMBER | VARIANT_BYTE | VARIANT_NAME |
| --- | --- | --- |
| 0x00 | LOW | LOW Variante |
| 0x01 | HIGH | HIGH Variante |
| 0xXY | -- | -- |

<a id="table-auswahl-fenster"></a>
### AUSWAHL_FENSTER

Dimensions: 6 rows × 2 columns

| ARGUMENT | BESCHREIBUNG |
| --- | --- |
| 0x00 | Vorgang abbrechen |
| 0x13 | Fahrerseite Hinten |
| 0x14 | Beifahrerseite Hinten |
| 0x22 | Fahrerseite und Beifahrerseite hinten |
| 0x40 | Alle |
| -- | unbekannter Diagnose-Mode |

<a id="table-fh-richtung"></a>
### FH_RICHTUNG

Dimensions: 10 rows × 3 columns

| TEXT | AUSWAHL_RICHTUNG | MODE_TEXT |
| --- | --- | --- |
| 0 | 0 | Fensterheber verfährt NICHT |
| 1 | 1 | Fensterheber verfährt AUF |
| 2 | 2 | Fensterheber verfährt ZU |
| 0x00 | 0 | Fensterheber verfährt NICHT |
| 0x01 | 1 | Fensterheber verfährt AUFn |
| 0x02 | 2 | Fensterheber verfährt ZU |
| AUS | 0 | Fensterheber verfährt NICHT |
| AUF | 1 | Fensterheber verfährt AUF |
| ZU | 2 | Fensterheber verfährt ZU |
| -- | 0xXY | unbekannter Diagnose-Mode |

<a id="table-fh-einlernen"></a>
### FH_EINLERNEN

Dimensions: 8 rows × 2 columns

| CODE | BESCHREIBUNG |
| --- | --- |
| 0x00 | NO INIT STARTED |
| 0x01 | Initialisierung laeuft |
| 0x02 | Initialisierung abgeschlossen |
| 0x03 | FEHLER: Busy |
| 0x04 | FEHLER: Abbruch durch Anwender |
| 0x05 | FEHLER: Reversierer |
| 0x06 | FEHLER: Init |
| 0xXY | undefiniert |

<a id="table-fh-denorm-fehlertexte"></a>
### FH_DENORM_FEHLERTEXTE

Dimensions: 26 rows × 2 columns

| NUMMER | TEXT |
| --- | --- |
| 0 | KEIN FEHLEREINTRAG |
| 1 | FAHRERSEITE - EEPROMFEHLER BEIM STARTUP |
| 2 | FAHRERSEITE - INTERFACE WURDE BEIM STARTUP NICHT BEDIENT |
| 3 | FAHRERSEITE - ÜBERFAHREN DER POSITION AF |
| 4 | FAHRERSEITE - ÜBERFAHREN DER POSITION GF |
| 5 | FAHRERSEITE - NICHT PLAUSIBLER ZUSTAND |
| 6 | FAHRERSEITE - DEFIZITCOUNTER ÜBERSCHRITTEN |
| 7 | FAHRERSEITE - RELAISKLEBER_1 |
| 8 | FAHRERSEITE - RELAISKLEBER_2 |
| 9 | FAHRERSEITE - HALLFEHLER |
| 10 | FAHRERSEITE - EXPLIZITES DENORMIEREN |
| 11 | FAHRERSEITE - TASKS WURDEN NICHT RECHTZEITIG AUFGERUFEN |
| 12 | FAHRERSEITE - HALLUNTERABTASTUNG |
| 101 | BEIFAHRERSEITE - EEPROMFEHLER BEIM STARTUP |
| 102 | BEIFAHRERSEITE - INTERFACE WURDE BEIM STARTUP NICHT BEDIENT |
| 103 | BEIFAHRERSEITE - ÜBERFAHREN DER POSITION AF |
| 104 | BEIFAHRERSEITE - ÜBERFAHREN DER POSITION GF |
| 105 | BEIFAHRERSEITE - NICHT PLAUSIBLER ZUSTAND |
| 106 | BEIFAHRERSEITE - DEFIZITCOUNTER ÜBERSCHRITTEN |
| 107 | BEIFAHRERSEITE - RELAISKLEBER_1 |
| 108 | BEIFAHRERSEITE - RELAISKLEBER_2 |
| 109 | BEIFAHRERSEITE - HALLFEHLER |
| 110 | BEIFAHRERSEITE - EXPLIZITES DENORMIEREN |
| 111 | BEIFAHRERSEITE - TASKS WURDEN NICHT RECHTZEITIG AUFGERUFEN |
| 112 | BEIFAHRERSEITE - HALLUNTERABTASTUNG |
| 0xXY | undefiniert |

<a id="table-fh-reversier-fehlertexte"></a>
### FH_REVERSIER_FEHLERTEXTE

Dimensions: 8 rows × 2 columns

| NUMMER | TEXT |
| --- | --- |
| 0 | KEIN FEHLEREINTRAG |
| 1 | FAHRERSEITE - REVERS_ISR |
| 2 | FAHRERSEITE - REVERS_BLOCK |
| 3 | FAHRERSEITE - REVERS_ISRDIAG |
| 101 | BEIFAHRERSEITE - REVERS_ISR |
| 102 | BEIFAHRERSEITE - REVERS_BLOCK |
| 103 | BEIFAHRERSEITE - REVERS_ISRDIAG |
| 0xXY | undefiniert |

<a id="table-fh-auswahl-baureihe"></a>
### FH_AUSWAHL_BAUREIHE

Dimensions: 2 rows × 3 columns

| WERT | ARGUMENT | BESCHREIBUNG |
| --- | --- | --- |
| 0 | E70 | E70 |
| 0xXY | undefiniert | undefiniert |

<a id="table-funktionaleadresse-lear"></a>
### FUNKTIONALEADRESSE_LEAR

Dimensions: 7 rows × 3 columns

| NR | F_ADR | F_ADR_TEXT |
| --- | --- | --- |
| 0xE9 | K-CAN | Karosserie-CAN Steuergeräte |
| 0xEA | PT-CAN | Powertrain-CAN Steuergeräte |
| 0xEB | SI | Sicherheits-BUS Steuergeräte |
| 0xEC | MOST | MOST-BUS Steuergeräte |
| 0xED | BOS oder CBS | Bedarfsorientierter Service |
| 0xEE | PERSONAL | Personalisierung |
| 0xEF | ALL | alle Steuergeräte |

<a id="table-digitalinputnrtexte"></a>
### DIGITALINPUTNRTEXTE

Dimensions: 33 rows × 4 columns

| DINNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | HECKKLAPPE_TASTER | Heckklappentaster (TOEHK)				  	 	 .CO_MICRO PIN 7,PORT B.6 | Keine Betätigung: 0, Taster Gedrückt: 1 |
| 0x01 | HECKSCHEIBE_TASTER | PL4 (E70):Taster Handschuhkasten/PL2-RED:Taster Heckscheibe(TOEHS) .CO_MICRO PIN 10,PORT D.6 | Keine Betätigung: 0, Taster Gedrückt: 1 |
| 0x02 | HECKKLAPPE_KONTAKT | Heckklappenkontakt (HKK)				  	 		 .CO_MICRO PIN  12,PORT B.0 | Geschlossen: 0, Offen: 1 |
| 0x03 | HECKSCHEIBE_KONTAKT | Heckscheibenkontakt (HSK)				  	 	 .CO_MICRO PIN  13,PORT B.1 | Geschlossen: 0, Offen: 1 |
| 0x04 | FRONTWISCHER_RSK | Frontwischer in Parkposition		  	 		 .PIN 134,PORT P6.5 | AUS RSK: 0, EIN RSK: 1 |
| 0x05 | HECKWISCHER_RSK | Heckwischer in Parkposition		  	 		 .PIN 121,PORT P5.11 | AUS RSK: 0, EIN RSK: 1 |
| 0x06 | DSC_BEFEHL | Sensor DSC-Taster  	 .PIN 94,PORT P4.0 | Keine Betätigung: 0, Taster Gedrückt: 1 |
| 0x07 | KUEHLMITTELSTAND | Sensor Kuehlmittelstand			  	 	 .PIN 124,PORT P5.14 | Zu niedrigem Füllstand: 0, Normales Füllstand: 1 |
| 0x08 | WASCHWASSERSTAND | Sensor Waschwasserstand					  	 		 .PIN 139,PORT P6.10 | Zu niedrigem Füllstand: 0, Normales Füllstand: 1 |
| 0x09 | HANDBREMSE_KONTAKT | Kontakt Handbremse						  	 	 .PIN 132,PORT P6.3 | Gelöst: 0, Angezogen: 1 |
| 0x0A | HECKWISCHER_DIAG | Relais Heckwischer (Diagnose)  					 .PIN 2,PORT P0.1 | AUS: 0, EIN: 1 |
| 0x0B | FRONTWISCHER_DIAG | Relais Frontwischer (Diagnose)       			  	 .PIN 57, PORT P2.10 | AUS: 0, EIN: 1 |
| 0x0C | FRONTWISCHER_GESCHW_DIAG | Geschwindigkeits-Relais Frontwischer (Diagnose)    			 .PIN 58, PORT P2.11 | AUS: 0, EIN: 1 |
| 0x0D | SRA_WASCHPUMPE | Scheinwerferreinigungsanlage (Diagnose)  	 		    		 .PIN 18,PORT P0.3 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x0E | HANDSCHUHKASTEN_DIAG | Handschuhkasten (Diagnose)          		  	 		 .PIN 136,PORT P6.7 | AUS: 0, EIN: 1 |
| 0x0F | HECKSCHEIBENHEIZUNG_DIAG | Heckscheibenheizung (Diagnose)          		  	 .PIN 131,PORT P6.2 | AUS: 0, EIN: 1 |
| 0x10 | HECKSCHEIBE_DIAG | Heckscheibenkontakt (Diagnose)          		  	 .CO_MICRO PIN 2,PORT D.4 | AUS: 0, EIN: 1 |
| 0x11 | HECKKLAPPE_DIAG | Heckklappenkontakt (Diagnose)          		  	 .CO_MICRO PIN 9,PORT D.5 | AUS: 0, EIN: 1 |
| 0x12 | ZV_VERRIEGELN_RELAIS_DIAG | Zentralverriegelung: Relais LOCK (Diagnose)     	  	 .PIN 12,PORT P0.9 | AUS: 0, EIN: 1 |
| 0x13 | ZV_ENTRIEGELN_RELAIS_DIAG | Zentralverriegelung: Relais UNLOCK (Diagnose)        	 .PIN 13,PORT P0.10 | AUS: 0, EIN: 1 |
| 0x14 | ZV_SICHERN_RELAIS_DIAG | Zentralverriegelung: Relais SECURE (Diagnose)        	 .PIN 14,PORT P0.11 | AUS: 0, EIN: 1 |
| 0x15 | ZV_SELEKTIV_ENTRIEGELN_RELAIS_DIAG | Zentralverriegelung: Relais UNLOCK Fahrerseite (Diagnose) 	 .PIN 36,PORT P1.13 | AUS: 0, EIN: 1 |
| 0x16 | FH_FATH_AUF_DIAG | Fensterheber: Relais OEFFNEN Fahrersite hinten (Diagnose) 	 .PIN 96,PORT P4.2 | AUS: 0, EIN: 1 |
| 0x17 | FH_FATH_ZU_DIAG | Fensterheber: Relais SCHLIESSEN Fahrersite hinten (Diagnose)	 .PIN 119,PORT P5.9 | AUS: 0, EIN: 1 |
| 0x18 | FH_BFTH_AUF_DIAG | Fensterheber: Relais OEFFNEN Beifahrersite hinten (Diagnose)  .PIN 110,PORT P5.0 | AUS: 0, EIN: 1 |
| 0x19 | FH_BFTH_ZU_DIAG | Fensterheber: Relais SCHLIESSEN Beifahrersite hinten (Diagnose) .PIN 112,PORT P5.2 | AUS: 0, EIN: 1 |
| 0x1A | TSR_IN | PL4 (E70):Dritte Sitzreihe/PL2-Red:MSA/PL2-Red (E90):EDC-Taster .PIN 3,PORT 0.2 | NICHT AKTIV: 1, AKTIV: 0 |
| 0x1B | KCAN_ERR | K-Can error indicator                 			 .PIN 11,PORT P0.8 | NICHT AKTIV: 1, AKTIV: 0 |
| 0x1C | EVV_HS_DIAG | Servotronik (EVV) High Side FET (Diagnose)       .PIN 34, PORT P1.11 | Überlastung oder Übertemperatur: 0, Normalbetrieb: 1 |
| 0x1D | EVV_LS_DIAG | Servotronik (EVV) Low Side FET (Diagnose)   	 .PIN 106,PORT P4.12 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x1E | 5V_SW_DIAG | Atmel 5V_SW Activation Diagnosis  				 .PIN 130, PORT P6.1 | AUS: 0, EIN: 1 |
| 0x1F | PTWAKE_IN | PT CAN Wake-Up Input line						 .CO_MICRO PIN 11,PORT D.7 | NICHT AKTIV: 0, AKTIV: 1 |
| 0xFF | UNKNOWN | unbekannte Digitaler Eingang |  |

<a id="table-digitaloutputnrtexte"></a>
### DIGITALOUTPUTNRTEXTE

Dimensions: 35 rows × 4 columns

| DOUTNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x01 | KOMPRESSOR_KUPPLUNG | Magnet-Kupplung                     		.PIN 111,PORT P5.1 | AUS: 0, EIN: 1 |
| 0x03 | 5V_SENSOR_ENABLE | 5V Sensor aktiv            			 	.PIN 129,PORT P6.0 | DISABLE: 0, ENABLE: 1 |
| 0x04 | WASSERVENTIL_FAHRER | Wasserventil 1 (Fahrerseite) 						.PIN 120,PORT P5.10 | CLOSED: 0, OPEN: 1  |
| 0x05 | WASSERVENTIL_BEIFAHRER | PL4 (E70):Wasserventil 2 (Beifahrer)/PL2-RED(E90_M3):EDC-LED 2.PIN 102,PORT P4.8 |  CLOSED: 0, OPEN: 1 |
| 0x06 | FRONTWASCHERPUMPE | Waschwasserpumpe vorne                      		.PIN 100,PORT P4.6 | AUS: 0, EIN: 1 |
| 0x07 | HECKWASCHERPUMPE | Waschwasserpumpe hinten                       		.PIN 101,PORT P4.7 | AUS: 0, EIN: 1 |
| 0x08 | SONNENROLLO_AUSGANG | PL2-Redesign (E90,E92): Ausgang Sonnenrollo | AUS: 0, Von EIN zu AUS: 5, NACH OBEN: 6, HERUNTER: 9 |
| 0x09 | SONNENROLLO_LOWTREIBER1 | PL2-Redesign (E90,E92): Sonnenrollo Mosfet Low Side 1.PIN 42,PORT P2.3 | AUS: 0, EIN: 1 |
| 0x0A | SONNENROLLO_HIGHTREIBER1 | PL2-RED (E90,E92):Sonnenrollo Mosfet High Side1/PL4 (E70):Handschuhkasten oeffnen.PIN 125,PORT P5.15 | AUS: 0, EIN: 1 |
| 0x0B | SONNENROLLO_LOWTREIBER2 | PL2-RED (E90,E92):Sonnenrollo Mosfet Low Side 2/PL2-RED (E91):Laderaumabdeckung/PL4 (E70):Handschuhkasten oeffnen.PIN 42,PORT P2.15 | AUS: 0, EIN: 1 |
| 0x0C | SONNENROLLO_HIGHTREIBER2 | PL2-RED (E90,E92):Sonnenrollo Mosfet High Side2/PL2-RED (E91):Laderaumabdeckung/PL4 (E70):Handschuhkasten oeffnen.PIN 28,PORT P1.5 | AUS: 0, EIN: 1 |
| 0x11 | WASCHDUESENHEIZUNG_AUßENSPIEGEL_AUSGANG | Aussenspiegel- und Waschduesenheizung        .PIN 138,PORT P6.9 | AUS: 0, EIN: 3 |
| 0x12 | EVV_LS | Servotronik (EVV) Low Side FET     		.PIN 135,PORT P6.6 | AUS: 0, EIN: 1 |
| 0x13 | 5V_SW_ON | 5V_SW_ON nicht erlaubt                    	.PIN 62,PORT P2.15 | AUS: 0, EIN: 1 |
| 0x14 | PT_WAKE_OUT | PT-CAN Wake Up signal                      .PIN 118,PORT P5.8 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x18 | ZUSATZWASSERPUMPE | Zusatzwasserpumpe                   	.PIN 105,PORT P4.11 | AUS 0, EIN 1 |
| 0x24 | HECKWISCHER | PL4 (E70): Relais Heckwischer/PL2-RED(E88): Manuelles Cabrio-Dach.PIN 1,PORT P0.0 | AUS: 0, EIN: 1 |
| 0x25 | FRONTWISCHER_AUSGANG | Ausgang Frontwischer | AUS: 0, Stufe1: 1, Stufe2: 3 |
| 0x26 | FRONTWISCHER | Relais Frontwischer (Low Speed)               .PIN 137,PORT P6.8 | AUS: 0, EIN: 1 |
| 0x27 | FRONTWISCHER_GESCHW | Geschwindigkeits-Relais Frontwischer  (High Speed)        .PIN 4,PORT P0.3 | AUS: 0, EIN: 1 |
| 0x28 | SRA | Relais Scheinwerferreinigungsanlage (SRA)                   	.PIN 7,PORT P0.4 | AUS: 0, EIN: 1 |
| 0x29 | ZV_AUSGANG | Ausgang Zentralverriegelung | Aus: 0, Entriegeln: 2, Selektiv Entriegeln: 6, Verriegeln: 12, Sichern: 13, Entsichern: 14 |
| 0x2A | ZV_SICHERN_RELAIS | Zentralverriegelung: Relais SECURE           	.PIN 22,PORT P1.1 | AUS: 0, EIN: 1 |
| 0x2B | ZV_ENTRIEGELN_RELAIS | Zentralverriegelung: Relais UNLOCK             	.PIN 8,PORT P0.5 | AUS: 0, EIN: 1 |
| 0x2C | ZV_VERRIEGELN_RELAIS | Zentralverriegelung: Relais LOCK      		 	.PIN 32,PORT P1.9 | AUS: 0, EIN: 1 |
| 0x2D | ZV_SELEKTIV_VERRIEGELN_RELAIS | Zentralverriegelung: Relais UNLOCK Fahrerseite		.PIN 31,PORT P1.8 | AUS: 0, EIN: 1 |
| 0x2E | HECKLAPPE_ENTRIEGELN_SCA | Relais Heckklappe / SofCloseAutomatik (SCA)                 	 	.PIN 107,PORT P4.13 | AUS: 0, EIN: 1 |
| 0x2F | HECKSCHEIBE | Relais Heckscheibe oeffnen                   .PIN 109,PORT P4.15 | AUS: 0, EIN: 1 |
| 0x30 | HECKSCHEIBENHEIZUNG | Relais Heckscheibenheizung               		.PIN 10,PORT P0.7 | AUS: 0, EIN: 1 |
| 0x31 | BISTABILRELAIS_ON. 100 ms max. Activation Time | Bistabiles-Relais ON      .PIN 9,PORT P0.6 | AUS: 0, EIN: 1 |
| 0x32 | BISTABILRELAIS_OFF. 100 ms max. Activation Time | Bistabiles-Relais OFF     .PIN 61,PORT P2.14 | AUS: 0, EIN: 1 |
| 0x33 | HECKBISTABILRELAIS_ON. 100 ms max. Activation Time | Heck-Bistabiles-Relais ON       .PIN 108,PORT P4.14 | AUS: 0, EIN: 1 |
| 0x34 | HECKBISTABILRELAIS_OFF. 100 ms max. Activation Time | Heck-Bistabiles-Relais OFF      .PIN 113,PORT P5.3 | AUS: 0, EIN: 1 |
| 0x35 | LADERRAUMABDECKUNG | Heckscheibe (PL2-Red E91). 2 Sekunden Aktivierungszeit bis vollstaendig geoeffnet | AUS: 0, EIN: 1 |
| 0xFF | UNKNOWN | unbekannter Digitaler Ausgang |  |

<a id="table-analoginputnrtexte"></a>
### ANALOGINPUTNRTEXTE

Dimensions: 28 rows × 4 columns

| AINNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | AC_KOMPRESSOR_DIAG | Klima-Kompressor (Diagnose)      	  .PIN 80,PORT P3.11 | MIN:0x029(0.2 V)..MAX:0x333(4 V) |
| 0x01 | DRUCKSENSOR | Drucksensor			   		  .PIN 74,PORT P3.7 | MIN:0x029(0.2 V)..MAX:0x333(4 V) |
| 0x02 | FH_BFT_SCHALTER | Taster Fensterheber Beifahrerseite	  .PIN 73,PORT P3.6 | 137(0x089)..373(0x175): DOWNAUTO(2), 374(0x176)..603(0x25B): DOWNMANUAL(1), 604(0x25C)..787(0x313): UPAUTO(4), 788(0x314)..945(0x3B1): UPMANUAL(3), 946(0x3B2)..1023(0x3FF): OFF(0) |
| 0x03 | FH_FATH_SCHALTER | Taster Fensterheber Fahrerseite hinten    .PIN 69,PORT P3.2 | 137(0x089)..373(0x175): DOWNAUTO(2), 374(0x176)..603(0x25B): DOWNMANUAL(1), 604(0x25C)..787(0x313): UPAUTO(4), 788(0x314)..945(0x3B1): UPMANUAL(3), 946(0x3B2)..1023(0x3FF): OFF(0) |
| 0x04 | FH_BFTH_SCHALTER | Taster Fensterheber Beiahrerseite hinten .PIN 68,PORT P3.1 | 137(0x089)..373(0x175): DOWNAUTO(2), 374(0x176)..603(0x25B): DOWNMANUAL(1), 604(0x25C)..787(0x313): UPAUTO(4), 788(0x314)..945(0x3B1): UPMANUAL(3), 946(0x3B2)..1023(0x3FF): OFF(0) |
| 0x05 | TANK_LI_WIDERSTAND | Tanksensor links 	  .PIN 70,PORT P3.3 | MIN:0x032(0.244 V)..MAX:0x350(4.145 V) |
| 0x06 | TANK_RE_WIDERSTAND | Tanksensor rechts	  .PIN 71,PORT P3.4 | MIN:0x032(0.244 V)..MAX:0x350(4.145 V) |
| 0x07 | EVV_SENSE | Sensor Ausgangsstrom Servotronik .PIN 72,PORT P3.5 | 0...0x3FF(1023) |
| 0x08 | KOMPRESSOR_KUPPLUNG_DIAG | Magnet-Kupplung (Diagnose)         .PIN 82,PORT P3.13 | MIN:0x029(0.2 V)..MAX:0x383(4,5 V) |
| 0x09 | FONDSCHICHTUNGSENSOR | Sensor Luftstrom hinten		   	  .PIN 83,PORT P3.14 | MIN:0x029(0.2 V)..MAX:0x333(4 V) |
| 0x0A | SONNENROLLO_STROM | Sensor Strom Sonnenrollo          .PIN 81,PORT P3.12 | MIN:0x029(0.2 V)..MAX:0x333(4 V) |
| 0x0B | BATTERIE_SPANNUNG | Batteriespannung             	  .PIN 67,PORT P3.0 | 0(0 V)...0x3FF(1023)(28.40 V) (HEX);Vbat=(HEX)*100/3605  [V] |
| 0x0C | 5V_SENSOR | 5V SENSOR                   	  .PIN 84,PORT P3.15 | MIN:0x00 (0 V)..MAX:0x3FF(5 V) |
| 0x0D | WASCHERPUMPE_DIAG | Waschwasserpumpe (Diagnose)              .PIN 77,PORT P3.8 | MIN:0x029(0.2 V)..MAX:0x383(4,5 V) |
| 0x0E | ZUSATZWASSERPUMPE_DIAG | Zusatzwasserpumpe (Diagnose)   .CO_MICRO PIN 26,PORT PC.3 | MIN:0x029(0.2 V)..MAX:0x333(4 V) |
| 0x0F | WASSERVENTIL_FAHRER_DIAG | Wasserventil 1 Fahrerseite (Diagnose)            .CO_MICRO PIN 25,PORT PC.2 | MIN:0x029(0.2 V)..MAX:0x383(4,5 V) |
| 0x10 | WASSERVENTIL_BEIFAHRER_DIAG | Wasserventil 2 Beifahrerseite (Diagnose)           .CO_MICRO PIN 27,PORT PC.4 | MIN:0x029(0.2 V)..MAX:0x383(4,5 V) |
| 0x11 | WASCHDUESENHEIZUNG_DIAG | Aussenspiegel- und Waschduesenheizung (Diagnose)         .CO_MICRO PIN 19,PORT ADC6 | MIN:0x029(0.2 V)..MAX:0x383(4,5 V) |
| 0x12 | KL30_FH_HI_LI_SENSE | PL4 (E70):Power Window RearDriver Motor Voltage Sense   .PIN 78,PORT P3.9 | PL4 (E70):0(0 V)...0x3FF(1023)(28.40 V) (HEX);Vbat=(HEX)*100/3605 [V] |
| 0x13 | KL30_FH_HI_RE_SENSE | PL4 (E70):Power Window RearPassenger Motor Voltage Sense.PIN 79,PORT P3.10 | PL4 (E70):0(0 V)...0x3FF(1023)(28.40 V) (HEX);Vbat=(HEX)*100/3605 [V] |
| 0x14 | FH_FATH_MFFHA_STROM_SENSE | PL2-RED (E93):Power Window RearDriver Current Sense 1(O_MFFHA) .CO_MICRO PIN 28,PORT PC.5 | 0...0x3FF(1023) |
| 0x15 | FH_FATH_MFFHZ_STROM_SENSE | PL2-RED (E93):Power Window RearDriver Current Sense 2(O_MFFHZ) .CO_MICRO PIN 23,PORT PC.0 | 0...0x3FF(1023) |
| 0x16 | FH_BFTH_MFBHA_STROM_SENSE | PL2-RED (E93):Power Window RearPassenger Current Sense 3(O_MFBHA) .CO_MICRO PIN 22,PORT ADC7 | 0...0x3FF(1023) |
| 0x17 | FH_BFTH_MFBHZ_STROM_SENSE | PL2-RED (E93):Power Window RearPassenger Current Sense 4(O_MFBHZ) .CO_MICRO PIN 24,PORT PC.1 | 0...0x3FF(1023) |
| 0x18 | AUCSENSOR | AUC Sensor PWM                    .PIN 17, PORT P0.12 | AUCSENSOR_PERIOD: 0..131 ms, AUCSENSOR_DUTY_CYCLE: 0..100 %; NORMAL: Period=20 ms (50 Hz) Duty-cycle=5%-95%, SHORT-GND: Period=0 Duty-cycle=0, OPEN-LOAD: Duty-cycle=0xFFFF |
| 0x19 | SITZHEIZUNG_FA_DIAG | Sitzheizung Fahrerseite (Diagnose)     .PIN 30, PORT P1.7 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x1A | SITZHEIZUNG_BF_DIAG | Sitzheizung Beifahrerseite (Diagnose)  .PIN 19, PORT P0.14 | NICHT AKTIV: 0, AKTIV: 1 |
| 0xFF | UNKNOWN | unbekannter Analoger Ausgang |  |

<a id="table-analogoutputnrtexte"></a>
### ANALOGOUTPUTNRTEXTE

Dimensions: 5 rows × 4 columns

| AOUTNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | KOMPRESSORVENTIL_PWM | PWM-Tastverhaeltnis Klima-Kompressor-Ventil  	.PIN 39,PORT P2.0 | 0...100 [%] |
| 0x03 | SITZHEIZUNG_FA_PWM | PWM-Tastverhaeltnis Sitzheizung Fahrer      .PIN 45,PORT P2.6 | OFF: 0 (40ms ON), STATE1: 1 (32ms ON, 8ms OFF), STATE2: 2 (20ms ON, 20ms OFF), STATE3: 3 (12ms ON, 28ms OFF) |
| 0x04 | SITZHEIZUNG_BF_PWM | PWM-Tastverhaeltnis Sitzheizung Beifahrer   .PIN 46,PORT P2.7 | OFF: 0 (40ms ON), STATE1: 1 (32ms ON, 8ms OFF), STATE2: 2 (20ms ON, 20ms OFF), STATE3: 3 (12ms ON, 28ms OFF) |
| 0x05 | EVV_HS_PWM | PWM-Tastverhaeltnis Servotronik (EVV) High Side FET .PIN 43,PORT P2.4 | 0...100 [%] |
| 0xFF | UNKNOWN | unbekannter Analoger Ausgang |  |

<a id="table-steuern-digital-verfahren"></a>
### STEUERN_DIGITAL_VERFAHREN

Dimensions: 28 rows × 3 columns

| ARGUMENT | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | Vorgang Abbrechen | Vorgang Abbrechen |
| 0x05 | FH_BF_MAUT_AUF | Fensterheber Beifahrerseite Maut oeffnen |
| 0x06 | FH_BF_AUF | Fensterheber Beifahrerseite oeffnen |
| 0x07 | FH_BF_MAUT_ZU | Fensterheber Beifahrerseite Maut schliessen |
| 0x08 | FH_BF_ZU | Fensterheber Beifahrerseite schliessen |
| 0x09 | FH_FAH_MAUT_AUF | Fensterheber Fahrerseite hinten Maut oeffnen |
| 0x0A | FH_FAH_AUF | Fensterheber Fahrerseite hinten oeffnen |
| 0x0B | FH_FAH_MAUT_ZU | Fensterheber Fahrerseite hinten Maut schliessen |
| 0x0C | FH_FAH_ZU | Fensterheber Fahrerseite hinten schliessen |
| 0x0D | FH_BFH_MAUT_AUF | Fensterheber Beifahrerseite hinten Maut oeffnen |
| 0x0E | FH_BFH_AUF | Fensterheber Beifahrerseite hinten oeffnen |
| 0x0F | FH_BFH_MAUT_ZU | Fensterheber Beifahrerseite hinten Maut schliessen |
| 0x10 | FH_BFH_ZU | Fensterheber Beifahrerseite hinten schliessen |
| 0x15 | FH_FAH_BFH_MAUT_AUF | Fensterheber Fahrerseite hinten und Beifahrerseite hinten Maut oeffnen |
| 0x16 | FH_FAH_BFH_AUF | Fensterheber Fahrerseite hinten Beifahrerseite hinten oeffnen |
| 0x17 | FH_FAH_BFH_MAUT_ZU | Fensterheber Fahrerseite hinten und Beifahrerseite hinten Maut schliessen |
| 0x18 | FH_FAH_BFH_ZU | Fensterheber Fahrerseite hinten Beifahrerseite hinten schliessen |
| 0x32 | SPIEGEL_HEIZUNG_EIN | Spiegelheizung |
| 0x40 | ZV_FA_ENTRIEGELT | Zentralverriegelung Fahrerseite entriegelt |
| 0x41 | ZV_BF_ENTRIEGELT | Zentralverriegelung Beifahrerseite entriegelt |
| 0x42 | ZV_FAH_ENTRIEGELT | Zentralverriegelung Fahrerseite hinten entriegelt |
| 0x43 | ZV_BFH_ENTRIEGELT | Zentralverriegelung Beifahrerseite hinten entriegelt |
| 0x44 | ZV_FA_VERRIEGELT | Zentralverriegelung Fahrerseite verriegelt |
| 0x45 | ZV_BF_VERRIEGELT | Zentralverriegelung Beifahrerseite verriegelt |
| 0x46 | ZV_FAH_VERRIEGELT | Zentralverriegelung Fahrerseite hinten verriegelt |
| 0x47 | ZV_BFH_VERRIEGELT | Zentralverriegelung Beifahrerseite hinten verriegelt |
| 0x48 | SOFTCLOSE_ZU | Zentralverriegelung Beifahrerseite hinten verriegelt |
| 0x94 | ROLLO_HECK_BLOCK | Sonnenrollo Heck |

<a id="table-zuordnung-can-id-sg"></a>
### ZUORDNUNG_CAN_ID_SG

Dimensions: 409 rows × 7 columns

| INDEX | CAN_ID_DEZ | CAN_ID_HEX | CAN_ID_NAME | DIAG_ID_DEZ | DIAG_ID_HEX | SG_NAME |
| --- | --- | --- | --- | --- | --- | --- |
| 002 | 981 | 0x3D5 | Status Zentralverriegelung CKM [4] | 64 | 0x40 | CAS |
| 003 | 253 | 0xFD | Steuerung Fensterheber BFTH [5] | 0 | 0x0 | JBBF |
| 004 | 957 | 0x3BD | Status Verbraucherabschaltung [2] | 114 | 0x72 | FRMFA |
| 005 | 1152 | 0x480 | Netzwerkmanagement | 0 | 0x0 | JBBF |
| 006 | 128 | 0x80 | SYNC [6] | 41 | 0x29 | EHB3 |
| 007 | 133 | 0x85 | Synchronisation SC VDA (4) | 41 | 0x29 | EHB3 |
| 008 | 168 | 0xA8 | Drehmoment 1 K-CAN (11) | 18 | 0x12 | DME1/DDE1 |
| 009 | 169 | 0xA9 | Drehmoment 2 [10] | 18 | 0x12 | DME1/DDE1 |
| 010 | 170 | 0xAA | Drehmoment 3 K-CAN [10] | 18 | 0x12 | DME1/DDE1 |
| 011 | 172 | 0xAC | Radmoment Antriebsstrang 2 (6) | 18 | 0x12 | DME1/DDE1 |
| 012 | 177 | 0xB1 | Drehmomentanforderung Lenkung [1] | 41 | 0x29 | EHB3 |
| 013 | 180 | 0xB4 | Radmoment Antriebsstrang 1 (5) | 18 | 0x12 | DME1/DDE1 |
| 014 | 181 | 0xB5 | Drehmomentanforderung EGS [9] | 24 | 0x18 | EGS_EL |
| 015 | 182 | 0xB6 | Drehmomentanforderung DSC [7] | 41 | 0x29 | EHB3 |
| 016 | 186 | 0xBA | Getriebedaten (22) | 24 | 0x18 | EGS_EL |
| 017 | 187 | 0xBB | Sollmomentanforderung [8] | 41 | 0x29 | EHB3 |
| 018 | 188 | 0xBC | Status Sollmomentumsetzung [7] | 25 | 0x19 | VGSG |
| 019 | 190 | 0xBE | Alive Zähler [12] | 35 | 0x23 | ARS_Modul |
| 020 | 191 | 0xBF | Anforderung Radmoment Antriebsstrang [6] | 41 | 0x29 | EHB3 |
| 021 | 192 | 0xC0 | Alive Zentrales Gateway [1] | 0 | 0x0 | JBBF |
| 022 | 193 | 0xC1 | Alive Zähler Telefon [3] | 54 | 0x36 | TEL_JAP/TEL_BPI |
| 023 | 193 | 0xC1 | Alive Zähler Telefon [3] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 024 | 196 | 0xC4 | Lenkradwinkel K-CAN [13] | 41 | 0x29 | EHB3 |
| 025 | 200 | 0xC8 | Lenkradwinkel Oben F-CAN [10] | 2 | 0x2 | SZL_LWS/SZL_LWS |
| 026 | 201 | 0xC9 | Lenkradwinkel Oben 2 F-CAN [4] | 2 | 0x2 | SZL_LWS |
| 027 | 206 | 0xCE | Radgeschwindigkeit F-CAN [6] | 41 | 0x29 | EHB3/EHB3 |
| 028 | 213 | 0xD5 | Anforderung Radmoment Bremse (7) | 41 | 0x29 | EHB3 |
| 029 | 215 | 0xD7 | Alive Zähler Sicherheit [2] | 1 | 0x1 | ACSM |
| 030 | 216 | 0xD8 | CLU1 VDA (4) | 37 | 0x25 | SC_VDA/RSC_VDA |
| 031 | 225 | 0xE1 | Radmoment Bremse (4) | 41 | 0x29 | EHB3 |
| 032 | 226 | 0xE2 | Status Zentralverriegelung BFT [11] | 0 | 0x0 | JBBF |
| 033 | 227 | 0xE3 | CLU2 VDA (4) | 37 | 0x25 | SC_VDA/RSC_VDA |
| 034 | 230 | 0xE6 | Status Zentralverriegelung BFTH [11] | 0 | 0x0 | JBBF |
| 035 | 234 | 0xEA | Status Zentralverriegelung FAT [11] | 0 | 0x0 | JBBF |
| 036 | 238 | 0xEE | Status Zentralverriegelung FATH [11] | 0 | 0x0 | JBBF |
| 037 | 242 | 0xF2 | Status Zentralverriegelung HK [13] | 0 | 0x0 | JBBF |
| 038 | 244 | 0xF4 | CLU3 VDA (3) | 37 | 0x25 | RSC_VDA |
| 039 | 247 | 0xF7 | Querdynamik ARS VDM [3] | 35 | 0x23 | ARS_Modul |
| 040 | 249 | 0xF9 | Vertikaldynamik VDM ARS [3] | 57 | 0x39 | VDM |
| 041 | 250 | 0xFA | Steuerung Fensterheber FAT [10] | 114 | 0x72 | FRMFA |
| 042 | 251 | 0xFB | Steuerung Fensterheber BFT [5] | 0 | 0x0 | JBBF |
| 043 | 252 | 0xFC | Steuerung Fensterheber FATH [5] | 0 | 0x0 | JBBF |
| 044 | 254 | 0xFE | Spannungen Höhenstandssensoren [3] | 57 | 0x39 | VDM |
| 045 | 280 | 0x118 | Austausch AFS DSC [10] | 22 | 0x16 | AFS |
| 046 | 286 | 0x11E | Regeleingriffe DSC_AFS [6] | 41 | 0x29 | EHB3 |
| 047 | 288 | 0x120 | Status Teilsollwerte AFS DSC 2 [2] | 22 | 0x16 | AFS |
| 048 | 298 | 0x12A | Sensor Daten ROSE [2] | 1 | 0x1 | ACSM_ROSE |
| 049 | 300 | 0x12C | Eingangsdaten ROSE [4] | 41 | 0x29 | EHB3 |
| 050 | 304 | 0x130 | Klemmenstatus [19] | 64 | 0x40 | CAS/CAS |
| 051 | 309 | 0x135 | Steuerung Crashabschaltung EKP [1] | 1 | 0x1 | ACSM |
| 052 | 357 | 0x165 | CLU Status VDA (4) | 37 | 0x25 | SC_VDA/RSC_VDA |
| 053 | 370 | 0x172 | Quittierung Anforderung Kombi [1] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 054 | 403 | 0x193 | Anzeige ACC DCC (5) | 41 | 0x29 | EHB3 |
| 055 | 404 | 0x194 | Bedienung Tempomat/ACC [13] | 2 | 0x2 | SZL_LWS |
| 056 | 408 | 0x198 | Bedienung Getriebewahlschalter 2 [3] | 94 | 0x5E | GWS |
| 057 | 414 | 0x19E | Status DSC K-CAN [19] | 41 | 0x29 | EHB3 |
| 058 | 416 | 0x1A0 | Geschwindigkeit K-CAN [14] | 41 | 0x29 | EHB3 |
| 059 | 418 | 0x1A2 | Getriebedaten 2 [6] | 24 | 0x18 | EGS_EL |
| 060 | 422 | 0x1A6 | Wegstrecke [6] | 41 | 0x29 | EHB3 |
| 061 | 423 | 0x1A7 | Stellanforderung EMF [4] | 41 | 0x29 | EHB3 |
| 062 | 426 | 0x1AA | Effekt ErgoCommander [10] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 063 | 428 | 0x1AC | Status ARS-Modul [13] | 35 | 0x23 | ARS_Modul |
| 064 | 436 | 0x1B4 | Status Kombi (15) | 96 | 0x60 | Kombi |
| 065 | 437 | 0x1B5 | Wärmestrom/Lastmoment Klima [14] | 120 | 0x78 | IHKA |
| 066 | 438 | 0x1B6 | Wärmestrom Motor [11] | 18 | 0x12 | DME1/DDE1 |
| 067 | 440 | 0x1B8 | Bedienung ErgoCommander [6] | 103 | 0x67 | ZBE |
| 068 | 450 | 0x1C2 | Abstandsmeldung PDC [5] | 100 | 0x64 | PDC |
| 069 | 451 | 0x1C3 | Abstandsmeldung 2 PDC [3] | 100 | 0x64 | PDC |
| 070 | 454 | 0x1C6 | Akustikmeldung PDC [5] | 100 | 0x64 | PDC |
| 071 | 464 | 0x1D0 | Motordaten [13] | 18 | 0x12 | DME1/DDE1 |
| 072 | 466 | 0x1D2 | Anzeige Getriebedaten [22] | 24 | 0x18 | EGS_EL |
| 073 | 470 | 0x1D6 | Bedienung Taster Audio/Telefon [12] | 2 | 0x2 | SZL_LWS/SZL_LWS |
| 074 | 472 | 0x1D8 | Bedienung Klima Luftverteilung FA [13] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 075 | 473 | 0x1D9 | Bedienung Taster M-Drive [2] | 2 | 0x2 | SZL_LWS/SZL_LWS |
| 076 | 474 | 0x1DA | Bedienung Klima Fernwirken [5] | 64 | 0x40 | CAS |
| 077 | 476 | 0x1DC | Bedienung Schichtung Sitzheizung [1] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 078 | 478 | 0x1DE | Bedienung Klima Fond [8] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 079 | 480 | 0x1E0 | Bedienung Klima Luftverteilung BF [7] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 080 | 482 | 0x1E2 | Bedienung Klima Front [11] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 081 | 483 | 0x1E3 | Bedienung Taster Innenbeleuchtung [2] | 86 | 0x56 | FZD |
| 082 | 487 | 0x1E7 | Bedienung Sitzheizung/Sitzklima FA [7] | 120 | 0x78 | IHKA |
| 083 | 488 | 0x1E8 | Bedienung Sitzheizung/Sitzklima BF [7] | 120 | 0x78 | IHKA |
| 084 | 490 | 0x1EA | Bedienung Lenksäulenverstellung [5] | 120 | 0x78 | IHKA |
| 085 | 491 | 0x1EB | Bedienung Aktivsitz FA [4] | 120 | 0x78 | IHKA |
| 086 | 492 | 0x1EC | Bedienung Aktivsitz BF [4] | 120 | 0x78 | IHKA |
| 087 | 494 | 0x1EE | Bedienung Lenkstockstaster [6] | 114 | 0x72 | FRMFA |
| 088 | 499 | 0x1F3 | Bedienung Sitzmemory FA [4] | 255 | 0xFF | Sender unbekannt |
| 089 | 502 | 0x1F6 | Blinken [6] | 114 | 0x72 | FRMFA |
| 090 | 504 | 0x1F8 | Bedienung SHD/MDS [1] | 86 | 0x56 | FZD |
| 091 | 508 | 0x1FC | Status AFS [4] | 22 | 0x16 | AFS |
| 092 | 510 | 0x1FE | Crash [12] | 1 | 0x1 | ACSM |
| 093 | 512 | 0x200 | Regelgeschwindigkeit Stufentempomat (8) | 18 | 0x12 | DME1/DDE1 |
| 094 | 513 | 0x201 | Status EMF K-CAN [2] | 42 | 0x2A | EMF |
| 095 | 514 | 0x202 | Dimmung [10] | 114 | 0x72 | FRMFA |
| 096 | 517 | 0x205 | Akustikanforderung Kombi [3] | 96 | 0x60 | Kombi |
| 097 | 518 | 0x206 | Steuerung Anzeige Shiftlights [1] | 18 | 0x12 | DME1 |
| 098 | 523 | 0x20B | Memoryverstellung [6] | 109 | 0x6D | SM_FA |
| 099 | 524 | 0x20C | Steuerung Lenksäule [4] | 109 | 0x6D | SM_FA |
| 100 | 525 | 0x20D | Position Lenksäule [5] | 120 | 0x78 | IHKA |
| 101 | 528 | 0x210 | Bedienung HUD [7] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 102 | 529 | 0x211 | Status HUD [7] | 61 | 0x3D | HUD |
| 103 | 530 | 0x212 | Höhenstände Luftfeder [8] | 56 | 0x38 | EHC |
| 104 | 538 | 0x21A | Lampenzustand [13] | 114 | 0x72 | FRMFA |
| 105 | 540 | 0x21C | Bedienung Night-Vision [2] | 98 | 0x62 | CCC_GW |
| 106 | 542 | 0x21E | Status Night-Vision [2] | 87 | 0x57 | NVC |
| 107 | 548 | 0x224 | Bedienung Taster NSW [2] | 114 | 0x72 | FRMFA |
| 108 | 550 | 0x226 | Regensensor-Wischergeschwindigkeit [8] | 86 | 0x56 | FZD |
| 109 | 552 | 0x228 | Bedienung Sonderfunktion [8] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 110 | 554 | 0x22A | Status BFS [10] | 110 | 0x6E | SM_BF |
| 111 | 554 | 0x22A | Status BFS [10] | 0 | 0x0 | JBBF |
| 112 | 556 | 0x22C | Bedienung Taster NSL [2] | 114 | 0x72 | FRMFA |
| 113 | 558 | 0x22E | Status BFSH [7] | 255 | 0xFF | Sender unbekannt |
| 114 | 562 | 0x232 | Status FAS [10] | 109 | 0x6D | SM_FA |
| 115 | 562 | 0x232 | Status FAS [10] | 0 | 0x0 | JBBF |
| 116 | 566 | 0x236 | Status FASH [7] | 255 | 0xFF | Sender unbekannt |
| 117 | 570 | 0x23A | Status Funkschlüssel [13] | 64 | 0x40 | CAS |
| 118 | 571 | 0x23B | Status Klima Front Erweitert [1] | 120 | 0x78 | IHKA |
| 119 | 573 | 0x23D | Anforderung Anzeige Klima [2] | 120 | 0x78 | IHKA |
| 120 | 574 | 0x23E | Status Klima Fond [11] | 121 | 0x79 | FKA |
| 121 | 578 | 0x242 | Status Klima Front [11] | 120 | 0x78 | IHKA |
| 122 | 582 | 0x246 | Status Klima Front Bedienteil [11] | 120 | 0x78 | IHKA |
| 123 | 584 | 0x248 | Status Rückfahrkamera [2] | 119 | 0x77 | RFK |
| 124 | 585 | 0x249 | Steuerung Rückfahrkamera [1] | 98 | 0x62 | CCC_GW |
| 125 | 586 | 0x24A | Status PDC [6] | 100 | 0x64 | PDC |
| 126 | 587 | 0x24B | Status Türsensoren [5] | 114 | 0x72 | FRMFA |
| 127 | 594 | 0x252 | Wischerstatus [8] | 0 | 0x0 | JBBF |
| 128 | 598 | 0x256 | Challenge Passive Access [10] | 64 | 0x40 | CAS |
| 129 | 600 | 0x258 | Status Transmission Passive Access [4] | 39 | 0x27 | PGS |
| 130 | 604 | 0x25C | Bedienung Klima Zusatzprogramme [2] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 131 | 622 | 0x26E | Steuerung FH/SHD Zentrale (Komfort) [10] | 64 | 0x40 | CAS |
| 132 | 638 | 0x27E | Status Verdeck Cabrio [7] | 255 | 0xFF | Sender unbekannt |
| 133 | 642 | 0x282 | Steuerung Sicherheitsfahrzeug 2 [6] | 255 | 0xFF | Sender unbekannt |
| 134 | 644 | 0x284 | Steuerung Fernstart Sicherheitsfahrzeug [8] | 64 | 0x40 | CAS |
| 135 | 646 | 0x286 | Steuerung Elektrochrom Abblenden [1] | 86 | 0x56 | FZD |
| 136 | 652 | 0x28C | Bedienung Taster Vertikaldynamik [2] | 94 | 0x5E | GWS |
| 137 | 656 | 0x290 | Steuerung Reaktion Wasserstoff-Fahrzeug [1] | 255 | 0xFF | Sender unbekannt |
| 138 | 658 | 0x292 | Steuerung Fernlicht-Assistent (3) | 95 | 0x5F | FLA |
| 139 | 670 | 0x29E | Steuerung Zentralverriegelung Sicherheitsfahrzeug [4] | 255 | 0xFF | Sender unbekannt |
| 140 | 671 | 0x29F | Fernbedienung FondCommander [5] | 64 | 0x40 | CAS |
| 141 | 672 | 0x2A0 | Steuerung Zentralverriegelung [10] | 64 | 0x40 | CAS |
| 142 | 674 | 0x2A2 | Bedienung Klima Standfunktionen [5] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 143 | 676 | 0x2A4 | Bedienung Personalisierung [8] | 96 | 0x60 | Kombi |
| 144 | 678 | 0x2A6 | Bedienung Wischertaster [12] | 2 | 0x2 | SZL_LWS/SZL_LWS |
| 145 | 690 | 0x2B2 | Raddrücke K-CAN [1] | 41 | 0x29 | EHB3 |
| 146 | 691 | 0x2B3 | Beschleunigungsdaten [3] | 41 | 0x29 | EHB3 |
| 147 | 692 | 0x2B4 | DWA-Alarm [4] | 86 | 0x56 | FZD |
| 148 | 694 | 0x2B6 | Steuerung Hupe DWA [3] | 86 | 0x56 | FZD |
| 149 | 696 | 0x2B8 | Bedienung Bordcomputer [3] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 150 | 697 | 0x2B9 | Bedienung RSE [1] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 151 | 698 | 0x2BA | Stoppuhr [3] | 96 | 0x60 | Kombi |
| 152 | 701 | 0x2BD | Anforderung Umschalten Anzeige [2] | 98 | 0x62 | CCC_GW |
| 153 | 702 | 0x2BE | Status Umschalten Anzeige [2] | 72 | 0x48 | VSW |
| 154 | 703 | 0x2BF | Steuerung Wasserventile [2] | 120 | 0x78 | IHKA |
| 155 | 704 | 0x2C0 | LCD-Leuchtdichte [7] | 96 | 0x60 | Kombi |
| 156 | 706 | 0x2C2 | Temperatur Ist Fond [2] | 121 | 0x79 | FKA |
| 157 | 714 | 0x2CA | Außentemperatur [9] | 96 | 0x60 | Kombi |
| 158 | 716 | 0x2CC | Steuerung Monitor Fond [2] | 38 | 0x26 | RSE |
| 159 | 718 | 0x2CE | Steuerung Monitor [4] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 160 | 719 | 0x2CF | Status Zusatzwasserpumpe [4] | 0 | 0x0 | JBBF |
| 161 | 720 | 0x2D0 | Status Sensor AUC [4] | 0 | 0x0 | JBBF |
| 162 | 721 | 0x2D1 | Status Beschlag Scheibe V [5] | 86 | 0x56 | FZD |
| 163 | 722 | 0x2D2 | Status Druck Kältekreislauf [5] | 0 | 0x0 | JBBF |
| 164 | 723 | 0x2D3 | Status Schichtung Fond [6] | 0 | 0x0 | JBBF |
| 165 | 725 | 0x2D5 | Status Heizung Heckscheibe [1] | 0 | 0x0 | JBBF |
| 166 | 726 | 0x2D6 | Status Ventil Klimakompressor [3] | 0 | 0x0 | JBBF |
| 167 | 730 | 0x2DA | Status Heckklappenlift [2] | 107 | 0x6B | HKL |
| 168 | 734 | 0x2DE | Steuerung Umschalten Anzeige [1] | 72 | 0x48 | VSW |
| 169 | 738 | 0x2E2 | Status Einstellung Video Night-Vision [1] | 87 | 0x57 | NVC |
| 170 | 739 | 0x2E3 | Status Einstellung Video Rückfahrkamera [1] | 119 | 0x77 | RFK |
| 171 | 740 | 0x2E4 | Status Anhänger [8] | 113 | 0x71 | AHM |
| 172 | 742 | 0x2E6 | Status Klima Luftverteilung FA [13] | 120 | 0x78 | IHKA |
| 173 | 746 | 0x2EA | Status Klima Luftverteilung BF [9] | 120 | 0x78 | IHKA |
| 174 | 752 | 0x2F0 | Status Klima Standfunktionen [12] | 120 | 0x78 | IHKA |
| 175 | 758 | 0x2F6 | Steuerung Licht [7] | 114 | 0x72 | FRMFA |
| 176 | 759 | 0x2F7 | Einheiten [10] | 96 | 0x60 | Kombi |
| 177 | 760 | 0x2F8 | Uhrzeit/Datum [12] | 96 | 0x60 | Kombi |
| 178 | 762 | 0x2FA | Sitzbelegung Gurtkontakte (15) | 1 | 0x1 | ACSM |
| 179 | 764 | 0x2FC | ZV und Klappenzustand [11] | 64 | 0x40 | CAS |
| 180 | 768 | 0x300 | Status RSE [1] | 38 | 0x26 | RSE |
| 181 | 772 | 0x304 | Status Gang [13] | 24 | 0x18 | EGS_EL |
| 182 | 774 | 0x306 | Fahrzeugneigung [2] | 114 | 0x72 | FRMFA |
| 183 | 776 | 0x308 | Status MSA [2] | 18 | 0x12 | DME1/DDE1 |
| 184 | 784 | 0x310 | Außentemperatur/Relativzeit [10] | 96 | 0x60 | Kombi |
| 185 | 785 | 0x311 | Nachtankmenge [3] | 96 | 0x60 | Kombi |
| 186 | 786 | 0x312 | Service Call Teleservice [2] | 96 | 0x60 | Kombi |
| 187 | 787 | 0x313 | Status Service Call Teleservice [3] | 54 | 0x36 | TEL_BPI |
| 188 | 787 | 0x313 | Status Service Call Teleservice [3] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 189 | 788 | 0x314 | Status Fahrlicht [9] | 86 | 0x56 | FZD |
| 190 | 790 | 0x316 | Bedienung Taster DSC [4] | 120 | 0x78 | IHKA |
| 191 | 791 | 0x317 | Bedienung Taster Einparkhilfen [2] | 120 | 0x78 | IHKA |
| 192 | 792 | 0x318 | Status Antennen Passive Access [7] | 39 | 0x27 | PGS |
| 193 | 793 | 0x319 | Bedienung Taster RDC (5) | 96 | 0x60 | Kombi |
| 194 | 794 | 0x31A | Bedienung Taster HDC [2] | 120 | 0x78 | IHKA |
| 195 | 795 | 0x31B | Bedienung Taster Heckklappe Innen [2] | 120 | 0x78 | IHKA |
| 196 | 796 | 0x31C | Status Reifendruck [6] | 32 | 0x20 | RDC |
| 197 | 797 | 0x31D | Status Reifenpannenanzeige [6] | 41 | 0x29 | EHB3 |
| 198 | 801 | 0x321 | Bedienung Taster Kamera BF [2] | 120 | 0x78 | IHKA |
| 199 | 806 | 0x326 | Status Dämpferprogramm [9] | 57 | 0x39 | VDM |
| 200 | 808 | 0x328 | Relativzeit [9] | 96 | 0x60 | Kombi |
| 201 | 813 | 0x32D | Anzeige HDC [3] | 41 | 0x29 | EHB3 |
| 202 | 814 | 0x32E | Status Klima Interne Regelinfo [6] | 120 | 0x78 | IHKA |
| 203 | 816 | 0x330 | Kilometerstand/Reichweite [5] | 96 | 0x60 | Kombi |
| 204 | 817 | 0x331 | Programmierung Stufentempomat [2] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 205 | 818 | 0x332 | Fahreranzeige Drehzahlbereich [4] | 18 | 0x12 | DME1/DDE1 |
| 206 | 821 | 0x335 | Status Elektrische Kraftstoffpumpe [3] | 23 | 0x17 | EKP |
| 207 | 822 | 0x336 | Anzeige Checkcontrol-Meldung (Rolle) [3] | 96 | 0x60 | Kombi |
| 208 | 823 | 0x337 | Status Kraftstoffregelung DME [1] | 18 | 0x12 | DME1 |
| 209 | 824 | 0x338 | Steuerung Anzeige Checkcontrol-Meldung [7] | 96 | 0x60 | Kombi |
| 210 | 825 | 0x339 | Status Anzeige Klima [2] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 211 | 826 | 0x33A | Status Monitor Front [3] | 115 | 0x73 | CID_C_H/CID_C |
| 212 | 828 | 0x33C | Status Monitor Fond 1 [3] | 116 | 0x74 | CID_C_R |
| 213 | 830 | 0x33E | Status Monitor Fond 2 [3] | 117 | 0x75 | CID_C_R_2 |
| 214 | 841 | 0x349 | Rohdaten Füllstand Tank (5) | 0 | 0x0 | JBBF |
| 215 | 843 | 0x34B | Status Sitzlehnenverriegelung FA [4] | 109 | 0x6D | SM_FA |
| 216 | 845 | 0x34D | Status Sitzlehnenverriegelung BF [2] | 110 | 0x6E | SM_BF |
| 217 | 847 | 0x34F | Status Kontakt Handbremse [4] | 255 | 0xFF | Sender unbekannt |
| 218 | 858 | 0x35A | Termin Condition Based Service [2] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 219 | 860 | 0x35C | Status Bordcomputer [5] | 96 | 0x60 | Kombi |
| 220 | 862 | 0x35E | Daten Bordcomputer (Reisedaten) [5] | 96 | 0x60 | Kombi |
| 221 | 864 | 0x360 | Daten Bordcomputer (Fahrtbeginn) [2] | 96 | 0x60 | Kombi |
| 222 | 866 | 0x362 | Daten Bordcomputer (Durchschnittswerte) [4] | 96 | 0x60 | Kombi |
| 223 | 868 | 0x364 | Daten Bordcomputer (Ankunft) [2] | 96 | 0x60 | Kombi |
| 224 | 870 | 0x366 | Anzeige Kombi/Externe Anzeige [3] | 96 | 0x60 | Kombi |
| 225 | 871 | 0x367 | Steuerung Anzeige Bedarfsorientierter Service [7] | 96 | 0x60 | Kombi |
| 226 | 884 | 0x374 | Radtoleranzabgleich [7] | 41 | 0x29 | EHB3 |
| 227 | 886 | 0x376 | Status Verschleiß Lamelle [3] | 25 | 0x19 | VGSG |
| 228 | 896 | 0x380 | Fahrgestellnummer [5] | 64 | 0x40 | CAS |
| 229 | 897 | 0x381 | Elektronischer Motorölmessstab [10] | 18 | 0x12 | DME1/DDE1 |
| 230 | 898 | 0x382 | Elektronischer Motorölmessstab M [1] | 18 | 0x12 | DME1/DDE1 |
| 231 | 904 | 0x388 | Fahrzeugtyp [14] | 64 | 0x40 | CAS |
| 232 | 907 | 0x38B | Status Batterie [1] | 18 | 0x12 | DME1/DDE1 |
| 233 | 910 | 0x38E | Startdrehzahl [1] | 18 | 0x12 | DME1/DDE1 |
| 234 | 914 | 0x392 | Status System AFS [3] | 22 | 0x16 | AFS |
| 235 | 916 | 0x394 | RDA Anfrage/Datenablage [5] | 96 | 0x60 | Kombi |
| 236 | 917 | 0x395 | Codierung Powermanagement [2] | 64 | 0x40 | CAS |
| 237 | 920 | 0x398 | Bedienung Fahrwerk [14] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 238 | 921 | 0x399 | Status M-Drive (3) | 18 | 0x12 | DME1 |
| 239 | 926 | 0x39E | Bedienung Uhrzeit/Datum [1] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 240 | 928 | 0x3A0 | Fahrzeugzustand [4] | 0 | 0x0 | JBBF |
| 241 | 931 | 0x3A3 | Anforderung Remote Services [2] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 242 | 940 | 0x3AC | Nachlaufzeit Klemme 30 fehlergesteuert [2] | 0 | 0x0 | JBBF |
| 243 | 944 | 0x3B0 | Status Gang Rückwärts [2] | 114 | 0x72 | FRMFA |
| 244 | 947 | 0x3B3 | Powermanagement Verbrauchersteuerung [9] | 18 | 0x12 | DME1/DDE1 |
| 245 | 948 | 0x3B4 | Powermanagement Batteriespannung [11] | 18 | 0x12 | DME1/DDE1 |
| 246 | 949 | 0x3B5 | Status Wasserventil [6] | 0 | 0x0 | JBBF |
| 247 | 950 | 0x3B6 | Position Fensterheber FAT [6] | 114 | 0x72 | FRMFA |
| 248 | 951 | 0x3B7 | Position Fensterheber FATH [5] | 0 | 0x0 | JBBF |
| 249 | 952 | 0x3B8 | Position Fensterheber BFT [6] | 114 | 0x72 | FRMFA |
| 250 | 953 | 0x3B9 | Position Fensterheber BFTH [5] | 0 | 0x0 | JBBF |
| 251 | 954 | 0x3BA | Position SHD [10] | 86 | 0x56 | FZD |
| 252 | 956 | 0x3BC | Position Fensterheber Sicherheitsfahrzeug [2] | 255 | 0xFF | Sender unbekannt |
| 253 | 958 | 0x3BE | Nachlaufzeit Stromversorgung [5] | 64 | 0x40 | CAS |
| 254 | 960 | 0x3C0 | Konfiguration FAS [3] | 109 | 0x6D | SM_FA |
| 255 | 961 | 0x3C1 | Konfiguration BFS [3] | 110 | 0x6E | SM_BF |
| 256 | 979 | 0x3D3 | Status Solarsensor [1] | 86 | 0x56 | FZD |
| 257 | 980 | 0x3D4 | Konfiguration Zentralverriegelung CKM [3] | 96 | 0x60 | Kombi |
| 258 | 982 | 0x3D6 | Konfiguration DWA CKM [1] | 96 | 0x60 | Kombi |
| 259 | 983 | 0x3D7 | Status DWA CKM [2] | 86 | 0x56 | FZD |
| 260 | 984 | 0x3D8 | Konfiguration RLS CKM [3] | 96 | 0x60 | Kombi |
| 261 | 985 | 0x3D9 | Status RLS CKM [4] | 86 | 0x56 | FZD |
| 262 | 986 | 0x3DA | Konfiguration Memorypositionen CKM [1] | 96 | 0x60 | Kombi |
| 263 | 987 | 0x3DB | Status Memorypositionen CKM [3] | 109 | 0x6D | SM_FA |
| 264 | 988 | 0x3DC | Konfiguration Licht CKM [3] | 96 | 0x60 | Kombi |
| 265 | 989 | 0x3DD | Status Licht CKM [4] | 114 | 0x72 | FRMFA |
| 266 | 990 | 0x3DE | Konfiguration Klima CKM [5] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 267 | 991 | 0x3DF | Status Klima CKM [6] | 120 | 0x78 | IHKA |
| 268 | 994 | 0x3E2 | Konfiguration Heckklappe CKM [1] | 98 | 0x62 | CHAMP_M_ASK2/CCC_GW |
| 269 | 995 | 0x3E3 | Status Heckklappe CKM [1] | 107 | 0x6B | HKL |
| 270 | 996 | 0x3E4 | Konfiguration Rückfahrkamera CKM [2] | 98 | 0x62 | CCC_GW |
| 271 | 997 | 0x3E5 | Status Rückfahrkamera CKM [2] | 119 | 0x77 | RFK |
| 272 | 1001 | 0x3E9 | Marker 1 [1] | 255 | 0xFF | Sender unbekannt |
| 273 | 1002 | 0x3EA | Marker 2 [3] | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 274 | 1003 | 0x3EB | Marker 3 [1] | 125 | 0x7D | Diagnosetool_PT_CAN |
| 275 | 1007 | 0x3EF | OBD Daten Motor [3] | 18 | 0x12 | DME1/DDE1 |
| 276 | 1008 | 0x3F0 | Konfiguration Licht Erweitert CKM [1] | 96 | 0x60 | Kombi |
| 277 | 1009 | 0x3F1 | Status Licht Erweitert CKM [1] | 114 | 0x72 | FRMFA |
| 278 | 1016 | 0x3F8 | Steuerung Klima Fond [3] | 120 | 0x78 | IHKA |
| 279 | 1018 | 0x3FA | Status Soll Klima Fond [1] | 121 | 0x79 | FKA |
| 280 | 1022 | 0x3FE | Anforderung CAN_Testtool SI-Bus [5] | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 281 | 1023 | 0x3FF | Übertragung Daten SI-Bus CAN_Testtool [5] | 255 | 0xFF | Sender unbekannt |
| 282 | 1153 | 0x481 | Netzwerkmanagement | 1 | 0x1 | ACSM |
| 283 | 1153 | 0x481 | Netzwerkmanagement | 1 | 0x1 | ACSM_ROSE |
| 284 | 1154 | 0x482 | Netzwerkmanagement | 2 | 0x2 | SZL_LWS |
| 285 | 1170 | 0x492 | Netzwerkmanagement | 18 | 0x12 | DDE1 |
| 286 | 1170 | 0x492 | Netzwerkmanagement | 18 | 0x12 | DME1 |
| 287 | 1174 | 0x496 | Netzwerkmanagement | 22 | 0x16 | AFS |
| 288 | 1175 | 0x497 | Netzwerkmanagement | 23 | 0x17 | EKP |
| 289 | 1176 | 0x498 | Netzwerkmanagement | 24 | 0x18 | EGS_EL |
| 290 | 1177 | 0x499 | Netzwerkmanagement | 25 | 0x19 | VGSG |
| 291 | 1179 | 0x49B | Netzwerkmanagement | 27 | 0x1B | VVT1 |
| 292 | 1182 | 0x49E | Netzwerkmanagement | 30 | 0x1E | VVT2 |
| 293 | 1184 | 0x4A0 | Netzwerkmanagement | 32 | 0x20 | RDC |
| 294 | 1187 | 0x4A3 | Netzwerkmanagement | 35 | 0x23 | ARS_Modul |
| 295 | 1189 | 0x4A5 | Netzwerkmanagement | 37 | 0x25 | RSC_VDA/SC_VDA |
| 296 | 1190 | 0x4A6 | Netzwerkmanagement | 38 | 0x26 | RSE |
| 297 | 1191 | 0x4A7 | Netzwerkmanagement | 39 | 0x27 | PGS |
| 298 | 1193 | 0x4A9 | Netzwerkmanagement | 41 | 0x29 | EHB3 |
| 299 | 1194 | 0x4AA | Netzwerkmanagement | 42 | 0x2A | EMF |
| 300 | 1201 | 0x4B1 | Netzwerkmanagement | 49 | 0x31 | MMC |
| 301 | 1206 | 0x4B6 | Netzwerkmanagement | 54 | 0x36 | TEL_BPI/TEL_JAP/TEL_MULF |
| 302 | 1207 | 0x4B7 | Netzwerkmanagement | 55 | 0x37 | AMP_HIFI/AMP_TOP |
| 303 | 1208 | 0x4B8 | Netzwerkmanagement | 56 | 0x38 | EHC |
| 304 | 1209 | 0x4B9 | Netzwerkmanagement | 57 | 0x39 | VDM |
| 305 | 1210 | 0x4BA | Netzwerkmanagement | 58 | 0x3A | KHM |
| 306 | 1211 | 0x4BB | Netzwerkmanagement | 59 | 0x3B | JNAV |
| 307 | 1212 | 0x4BC | Netzwerkmanagement | 60 | 0x3C | CDC |
| 308 | 1213 | 0x4BD | Netzwerkmanagement | 61 | 0x3D | HUD |
| 309 | 1216 | 0x4C0 | Netzwerkmanagement | 64 | 0x40 | CAS |
| 310 | 1221 | 0x4C5 | Netzwerkmanagement | 69 | 0x45 | RLS |
| 311 | 1224 | 0x4C8 | Netzwerkmanagement | 72 | 0x48 | VSW |
| 312 | 1227 | 0x4CB | Netzwerkmanagement | 75 | 0x4B | VM |
| 313 | 1232 | 0x4D0 | Netzwerkmanagement | 80 | 0x50 | Notstrom-Sirene |
| 314 | 1235 | 0x4D3 | Netzwerkmanagement | 83 | 0x53 | IBOC |
| 315 | 1236 | 0x4D4 | Netzwerkmanagement | 84 | 0x54 | SDARS |
| 316 | 1237 | 0x4D5 | Netzwerkmanagement | 85 | 0x55 | ISpeechBox |
| 317 | 1238 | 0x4D6 | Netzwerkmanagement | 86 | 0x56 | FZD |
| 318 | 1239 | 0x4D7 | Netzwerkmanagement | 87 | 0x57 | NVC |
| 319 | 1243 | 0x4DB | Netzwerkmanagement | 91 | 0x5B | DAB |
| 320 | 1246 | 0x4DE | Netzwerkmanagement | 94 | 0x5E | GWS |
| 321 | 1247 | 0x4DF | Netzwerkmanagement | 95 | 0x5F | FLA |
| 322 | 1248 | 0x4E0 | Netzwerkmanagement | 96 | 0x60 | Kombi |
| 323 | 1250 | 0x4E2 | Netzwerkmanagement | 98 | 0x62 | CCC_GW/CHAMP_M_ASK2 |
| 324 | 1251 | 0x4E3 | Netzwerkmanagement | 99 | 0x63 | CCC_MM |
| 325 | 1252 | 0x4E4 | Netzwerkmanagement | 100 | 0x64 | PDC |
| 326 | 1255 | 0x4E7 | Netzwerkmanagement | 103 | 0x67 | ZBE |
| 327 | 1259 | 0x4EB | Netzwerkmanagement | 107 | 0x6B | HKL |
| 328 | 1261 | 0x4ED | Netzwerkmanagement | 109 | 0x6D | SM_FA |
| 329 | 1262 | 0x4EE | Netzwerkmanagement | 110 | 0x6E | SM_BF |
| 330 | 1265 | 0x4F1 | Netzwerkmanagement | 113 | 0x71 | AHM |
| 331 | 1266 | 0x4F2 | Netzwerkmanagement | 114 | 0x72 | FRMFA/FRMFA_ALC |
| 332 | 1267 | 0x4F3 | Netzwerkmanagement | 115 | 0x73 | CID_C/CID_C_H |
| 333 | 1268 | 0x4F4 | Netzwerkmanagement | 116 | 0x74 | CID_C_R |
| 334 | 1269 | 0x4F5 | Netzwerkmanagement | 117 | 0x75 | CID_C_R_2 |
| 335 | 1271 | 0x4F7 | Netzwerkmanagement | 119 | 0x77 | RFK |
| 336 | 1272 | 0x4F8 | Netzwerkmanagement | 120 | 0x78 | IHKA |
| 337 | 1273 | 0x4F9 | Netzwerkmanagement | 121 | 0x79 | FKA |
| 338 | 1277 | 0x4FD | Netzwerkmanagement | 125 | 0x7D | Diagnosetool_PT_CAN |
| 339 | 1278 | 0x4FE | Netzwerkmanagement | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 340 | 1280 | 0x500 | Datentransfer [1] | 255 | 0xFF | Sender unbekannt |
| 341 | 1289 | 0x509 | Netzwerkmanagement | 137 | 0x89 | XE_HDLI_LH_ALC |
| 342 | 1290 | 0x50A | Netzwerkmanagement | 138 | 0x8A | XE_HDLI_RH_ALC |
| 343 | 1291 | 0x50B | Netzwerkmanagement | 139 | 0x8B | CNV |
| 344 | 1317 | 0x525 | Netzwerkmanagement | 165 | 0xA5 | EDCS_VL |
| 345 | 1318 | 0x526 | Netzwerkmanagement | 166 | 0xA6 | EDCS_VR |
| 346 | 1319 | 0x527 | Netzwerkmanagement | 167 | 0xA7 | EDCS_HL |
| 347 | 1320 | 0x528 | Netzwerkmanagement | 168 | 0xA8 | EDCS_HR |
| 348 | 1393 | 0x571 | Netzwerkmanagement | 241 | 0xF1 | Diagnosedose/D_CAN_Tester |
| 349 | 1408 | 0x580 | Dienste | 0 | 0x0 | JBBF |
| 350 | 1409 | 0x581 | Dienste | 1 | 0x1 | ACSM/ACSM_ROSE |
| 351 | 1410 | 0x582 | Dienste | 2 | 0x2 | SZL_LWS |
| 352 | 1426 | 0x592 | Dienste | 18 | 0x12 | DDE1/DME1 |
| 353 | 1430 | 0x596 | Dienste | 22 | 0x16 | AFS |
| 354 | 1431 | 0x597 | Dienste | 23 | 0x17 | EKP |
| 355 | 1432 | 0x598 | Dienste | 24 | 0x18 | EGS_EL |
| 356 | 1433 | 0x599 | Dienste | 25 | 0x19 | VGSG |
| 357 | 1435 | 0x59B | Dienste | 27 | 0x1B | VVT1 |
| 358 | 1438 | 0x59E | Dienste | 30 | 0x1E | VVT2 |
| 359 | 1440 | 0x5A0 | Dienste | 32 | 0x20 | RDC |
| 360 | 1443 | 0x5A3 | Dienste | 35 | 0x23 | ARS_Modul |
| 361 | 1445 | 0x5A5 | Dienste | 37 | 0x25 | RSC_VDA/SC_VDA |
| 362 | 1446 | 0x5A6 | Dienste | 38 | 0x26 | RSE |
| 363 | 1447 | 0x5A7 | Dienste | 39 | 0x27 | PGS |
| 364 | 1449 | 0x5A9 | Dienste | 41 | 0x29 | EHB3 |
| 365 | 1450 | 0x5AA | Dienste | 42 | 0x2A | EMF |
| 366 | 1457 | 0x5B1 | Dienste | 49 | 0x31 | MMC |
| 367 | 1462 | 0x5B6 | Dienste | 54 | 0x36 | TEL_BPI/TEL_JAP/TEL_MULF |
| 368 | 1463 | 0x5B7 | Dienste | 55 | 0x37 | AMP_HIFI/AMP_TOP |
| 369 | 1464 | 0x5B8 | Dienste | 56 | 0x38 | EHC |
| 370 | 1465 | 0x5B9 | Dienste | 57 | 0x39 | VDM |
| 371 | 1466 | 0x5BA | Dienste | 58 | 0x3A | KHM |
| 372 | 1467 | 0x5BB | Dienste | 59 | 0x3B | JNAV |
| 373 | 1468 | 0x5BC | Dienste | 60 | 0x3C | CDC |
| 374 | 1469 | 0x5BD | Dienste | 61 | 0x3D | HUD |
| 375 | 1472 | 0x5C0 | Dienste | 64 | 0x40 | CAS |
| 376 | 1477 | 0x5C5 | Dienste | 69 | 0x45 | RLS |
| 377 | 1480 | 0x5C8 | Dienste | 72 | 0x48 | VSW |
| 378 | 1483 | 0x5CB | Dienste | 75 | 0x4B | VM |
| 379 | 1488 | 0x5D0 | Dienste | 80 | 0x50 | Notstrom-Sirene |
| 380 | 1491 | 0x5D3 | Dienste | 83 | 0x53 | IBOC |
| 381 | 1492 | 0x5D4 | Dienste | 84 | 0x54 | SDARS |
| 382 | 1493 | 0x5D5 | Dienste | 85 | 0x55 | ISpeechBox |
| 383 | 1494 | 0x5D6 | Dienste | 86 | 0x56 | FZD |
| 384 | 1495 | 0x5D7 | Dienste | 87 | 0x57 | NVC |
| 385 | 1499 | 0x5DB | Dienste | 91 | 0x5B | DAB |
| 386 | 1502 | 0x5DE | Dienste | 94 | 0x5E | GWS |
| 387 | 1503 | 0x5DF | Dienste | 95 | 0x5F | FLA |
| 388 | 1504 | 0x5E0 | Dienste | 96 | 0x60 | Kombi |
| 389 | 1506 | 0x5E2 | Dienste | 98 | 0x62 | CCC_GW/CHAMP_M_ASK2 |
| 390 | 1507 | 0x5E3 | Dienste | 99 | 0x63 | CCC_MM |
| 391 | 1508 | 0x5E4 | Dienste | 100 | 0x64 | PDC |
| 392 | 1511 | 0x5E7 | Dienste | 103 | 0x67 | ZBE |
| 393 | 1515 | 0x5EB | Dienste | 107 | 0x6B | HKL |
| 394 | 1517 | 0x5ED | Dienste | 109 | 0x6D | SM_FA |
| 395 | 1518 | 0x5EE | Dienste | 110 | 0x6E | SM_BF |
| 396 | 1521 | 0x5F1 | Dienste | 113 | 0x71 | AHM |
| 397 | 1522 | 0x5F2 | Dienste | 114 | 0x72 | FRMFA/FRMFA_ALC |
| 398 | 1523 | 0x5F3 | Dienste | 115 | 0x73 | CID_C/CID_C_H |
| 399 | 1524 | 0x5F4 | Dienste | 116 | 0x74 | CID_C_R |
| 400 | 1525 | 0x5F5 | Dienste | 117 | 0x75 | CID_C_R_2 |
| 401 | 1527 | 0x5F7 | Dienste | 119 | 0x77 | RFK |
| 402 | 1528 | 0x5F8 | Dienste | 120 | 0x78 | IHKA |
| 403 | 1529 | 0x5F9 | Dienste | 121 | 0x79 | FKA |
| 404 | 1533 | 0x5FD | Dienste | 125 | 0x7D | Diagnosetool_PT_CAN |
| 405 | 1534 | 0x5FE | Dienste | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 406 | 1545 | 0x609 | Dienste | 137 | 0x89 | XE_HDLI_LH_ALC |
| 407 | 1546 | 0x60A | Dienste | 138 | 0x8A | XE_HDLI_RH_ALC |
| 408 | 1547 | 0x60B | Dienste | 139 | 0x8B | CNV |
| 409 | 1573 | 0x625 | Dienste | 165 | 0xA5 | EDCS_VL |
| 410 | 1574 | 0x626 | Dienste | 166 | 0xA6 | EDCS_VR |
