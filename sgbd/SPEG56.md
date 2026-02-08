# SPEG56.prg

- Jobs: [112](#jobs)
- Tables: [45](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | SPEG |
| ORIGIN | MSF MSF Alexander Vrchoticky |
| REVISION | 4.010 |
| AUTHOR | Lear Corporation Entwicklung Arseni Martínez, Lear Corporation Entwicklung Carme Tàpias, Lear Corporation Entwicklung Israel Revert, Lear Corporation Entwicklung Sergi Garriga |
| COMMENT | SGBD of SPEG for R56 |
| PACKAGE | 1.30 |
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
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
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
- [READ_ENERGY_SAVING_MODE](#job-read-energy-saving-mode) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [_READ_MEMORY_BY_ADDRESS](#job-read-memory-by-address) - Selected MEMORY reading by Address KWP 2000: $23  ReadMemoryByAddress KWP 2000: $02  External EEPROM KWP 2000: $04  Internal RAM
- [_WRITE_MEMORY_BY_ADDRESS](#job-write-memory-by-address) - Selected MEMORY writing by Address KWP 2000: $3D  WriteMemoryByAddress KWP 2000: $02  External EEPROM KWP 2000: $04  Internal RAM
- [_READ_DISP_EE](#job-read-disp-ee) - Read EEPROM EE Struct and Disp Flags KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C000 commonProjectSpecific
- [_WRITE_DISP_EE](#job-write-disp-ee) - Write EEPROM EE Struct and Disp Flags KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFFF commonProjectSpecific
- [_READ_BRIF](#job-read-brif) - Lear specific Job for reading BRIF from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C001 commonProjectSpecific
- [_READ_ZIF](#job-read-zif) - Lear specific Job for reading ZIF from RAM KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C002 commonProjectSpecific
- [_READ_LENGTH_DIAG_BUFFER](#job-read-length-diag-buffer) - Read Diag Buffer Lenth KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $C003 commonProjectSpecific
- [STATUS_VERSION_GATEWAYMODULES](#job-status-version-gatewaymodules) - Lesen der Versionsnummer der Gateway software, gateway tabelle, software version KWP2000: $21 ReadDataByLocalIdentifier $6F RecordLocalId Modus  : Default
- [_SLEEP_MODE_FUNKTIONAL](#job-sleep-mode-funktional) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Inputs $01 ReportCurrentState
- [STATUS_DIGITAL_OUTPUTS](#job-status-digital-outputs) - Auslesen der Stati von den digitalen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Outputs $01 ReportCurrentState
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Inputs $01 ReportCurrentState
- [STATUS_ANALOG_OUTPUTS](#job-status-analog-outputs) - Auslesen der Stati von den analogen Ausgaengen KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Outputs $01 ReportCurrentState
- [STEUERN_DIGITAL_INPUT](#job-steuern-digital-input) - Digitale Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $07 ShortTermAdjustment
- [STEUERN_DIGITAL_OUTPUT](#job-steuern-digital-output) - Digitale Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $02 Digitale Ouput $07 ShortTermAdjustment
- [STEUERN_ANALOG_INPUT](#job-steuern-analog-input) - Analoge Input direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $03 Analoge Input $07 ShortTermAdjustment
- [STEUERN_ANALOG_OUTPUT](#job-steuern-analog-output) - Analoge Output direkt ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $04 Analoge Output $07 ShortTermAdjustment
- [STEUERN_BEENDEN](#job-steuern-beenden) - Kontrolle an SPEG zurueckgeben KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $02 Digitale Output $03 Analoge Input $04 Analoge Output $00 ReturnControToECU
- [_STATUS_VAR_CAN_GENERAL](#job-status-var-can-general) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $00 GENERAL
- [_STATUS_VAR_CAN_WWS](#job-status-var-can-wws) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $01 WWS (Wiper-Washer System)
- [_STATUS_VAR_CAN_ZVS](#job-status-var-can-zvs) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $02 ZVS (Central Locking System)
- [_STATUS_VAR_CAN_DWA](#job-status-var-can-dwa) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $03 DWA (Anti-Theft Alarm System)
- [_STATUS_VAR_CAN_PH_KOMBI](#job-status-var-can-ph-kombi) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $04 PH_KOMBI (Peripherics Kombi)
- [_STATUS_VAR_CAN_PH_MISC](#job-status-var-can-ph-misc) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $05 PH_MISC (Peripherics Miscelaneous)
- [_STATUS_VAR_CAN_ACH](#job-status-var-can-ach) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $07 ACH (Air Conditioning / Heating)
- [_STATUS_VAR_CAN_PIA](#job-status-var-can-pia) - Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $09 PIA (Personalization, Individualization, Adaption)
- [_STATUS_VAR_IAP_GENERAL](#job-status-var-iap-general) - Auslesen der Stati von den Internen Application Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables Application $01 ReportCurrentState $00 GENERAL
- [_STATUS_VAR_IAP_WWS](#job-status-var-iap-wws) - Auslesen der Stati von den Internen Application Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables Application $01 ReportCurrentState $01 WWS (Wiper-Washer System)
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_1](#job-status-historienspeicher-lesen-block-1) - EnergieDatenSpeicher Teil 1 -Einschlafverhinderer- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE1 commonProjectSpecific
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_2](#job-status-historienspeicher-lesen-block-2) - EnergieDatenSpeicher Teil 2 -Wecker- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific
- [STEUERN_HISTORIENSPEICHER_LOESCHEN](#job-steuern-historienspeicher-loeschen) - EnergieDatenSpeicher Teil 1 und TEIL 2 loeschen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE0 commonProjectSpecific
- [_SLEEP_MODE_LEAR](#job-sleep-mode-lear) - Send ECU to Sleep Mode without waiting the busses to stop KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $02 Specific Lear Modus  : Default
- [_STATUS_LEAR_VERSIONS](#job-status-lear-versions) - Reading of the internal LEAR Application Software Version Lesen der internen Versionsnummer der Applikationssoftware KWP2000: $21 ReadDataByLocalIdentifier $70 RecordLocalId
- [AIF_LESEN_READECU](#job-aif-lesen-readecu) - Auslesen des Anwender Informations Feldes KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default
- [STATUS_LESEN_WISCHERTASTER](#job-status-lesen-wischertaster) - Auslesen des Wischertasterstatus KWP2000: 0x23 ReadMemoryByAddress
- [SG_INIT](#job-sg-init) - RLS_Initialisation KWP2000: $3D $00 $08 $20 $00 $01 $FF WriteMemoryByAddress
- [RLS_IDENT](#job-rls-ident) - KWP2000:  1. READ LEAR VERSION $21 $70 ReadDataByLocalIdentifier 2. LEAR VERSION &lt;V6.2.0  -&gt; $22 $16 $01 ReadDataByLocalIdentifier READ VERSION &gt;=V6.2.0 -&gt; $21 $A3 ReadDataByLocalIdentifier
- [STATUS_LESEN_RLS](#job-status-lesen-rls) - KWP2000: $30 $5501 InputOutputControlByLocalID
- [C_AEI_LESEN_RLS](#job-c-aei-lesen-rls) - RLS Aenderungsindex der Codierdaten lesen KWP2000: $21 $A0 ReadDataByLocalIdentifier
- [C_FG_LESEN_RLS](#job-c-fg-lesen-rls) - RLS Fahrgestellnummer lesen KWP2000: $21 $A1 ReadDataByLocalIdentifier
- [C_AEI_SCHREIBEN_RLS](#job-c-aei-schreiben-rls) - KWP2000: $3B $A0 WriteDataByLocalIdentifier
- [C_FG_SCHREIBEN_RLS](#job-c-fg-schreiben-rls) - KWP2000: $3B $A1 WriteDataByLocalIdentifier
- [C_AEI_AUFTRAG_RLS](#job-c-aei-auftrag-rls) - KWP2000: $3B $A0 WriteDataByLocalIdentifier and $21 $A0 ReadDataByLocalIdentifier ANSDERUNGSINDEX examples: 31 32 (12) 61 62 (ab)
- [C_FG_AUFTRAG_RLS](#job-c-fg-auftrag-rls) - KWP2000: $3B $A1 WriteDataByLocalIdentifier and $21 $A1 ReadDataByLocalIdentifier FAHRGESTELLNR examples: 31 32 33 34 35 36 37 (1234567) 61 62 63 64 65 66 67(abcdefg)
- [_LEAR_PLx_EOL_CONFIGURATION](#job-lear-plx-eol-configuration) - Configuration for the LEAR End of Line KWP2000: $3B WriteDataByLocalIdentifier $7A RecordLocalId
- [READ_VARIANT](#job-read-variant) - Lesen der Variante der Plattine KWP2000: $21 ReadDataByLocalIdentifier $6E RecordLocalId Modus  : Default
- [STEUERN_WASCHDUESE_AUSSENSPIEGEL](#job-steuern-waschduese-aussenspiegel) - Schreiben die Waschduese und Aussenspiegel parameter KWP2000: $3B WriteDataByLocalIdentifier $79 RecordLocalId
- [_EEPROM_INIT](#job-eeprom-init) - Initialise the EEPROM KWP2000: $3B WriteDataByLocalIdentifier $7E RecordLocalId
- [_PERFORMANCE_ANALYSIS](#job-performance-analysis) - Reading the Performing Analysis KWP2000: $21 ReadDataByLocalIdentifier $6C RecordLocalId Modus  : Default
- [STATUS_DWA_INTERN](#job-status-dwa-intern) - Readout of the application status of the DWA KWP2000: $21 ReadDataByLocalIdentifier $A2 identifier of the DWA_STS
- [_READ_WAKEUP_REASON](#job-read-wakeup-reason) - Returns the last wake-up reason KWP2000: $21 ReadDataByLocalIdentifier $71 RecordLocalId
- [STEUERN_DWA_IRS_SELFTEST](#job-steuern-dwa-irs-selftest) - Self Test of the INRS DWA KWP2000: $31 StartRoutineByLocalIdentifier $04 SelfTest $00 INRS DWA Modus  : Default
- [STEUERN_DWA_NG_SELFTEST](#job-steuern-dwa-ng-selftest) - Self Test of the NG DWA KWP2000: $31 StartRoutineByLocalIdentifier $04 SelfTest $01 NG DWA Modus  : Default
- [STATUS_ALARMTRIGGER](#job-status-alarmtrigger) - Return the status of every trigger of the DWA KWP2000: $21 ReadDataByLocalIdentifier $A4 identifier of the STATUS_ALARMTRIGGER

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

<a id="job-hs-lesen"></a>
### HS_LESEN

Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-lesen-detail"></a>
### HS_LESEN_DETAIL

Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Historycode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
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

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default

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

<a id="job-sensoren-anzahl-lesen"></a>
### SENSOREN_ANZAHL_LESEN

Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_ANZAHL | long | Anzahl der intelligenten Subbussensoren |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sensoren-ident-lesen"></a>
### SENSOREN_IDENT_LESEN

Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
| SENSOR_BMW_NR | string | BMW-Teilenummer des Sensors |
| SENSOR_PART_NR | string | Teilenummer des Sensors optional wenn SENSOR_BMW_NR gueltig wenn vom Teilenummer vom Sensor nicht verfuegbar dann '--' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

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

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Inputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HECKWISCHER_2_RSK_EIN | int | Heckwischer 2 Rückstellkontakt Rear Wiper 2 Park Position 0: HeckWischer im RSK, 1: HeckWischer nicht im RSK 0: IN PARK POSITION, 1: OUT PARK POSITION Wert am Pin umgekehrt! Actual value inverted! PIN 27, PORT P1.4 |
| STAT_MSA_TASTER_EIN | int | Motor Start Automatic Switch 0: KEINE BETÄTIGUNG, 1: TASTER GEDRÜCKT 0: NOT PUSHED, 1: PUSHED PIN 29, PORT P1.6 |
| STAT_SPORT_TASTER_EIN | int | SPORT Switch 0: KEINE BETÄTIGUNG, 1: TASTER GEDRÜCKT 0: NOT PUSHED, 1: PUSHED Wert am Pin umgekehrt! Actual value inverted! PIN 30, PORT P1.7 |
| STAT_HANDBREMSE_KONTAKT_EIN | int | Handbrake Switch 0: KEINE BETÄTIGUNG, 1: TASTER GEDRÜCKT 0: NOT PUSHED(Handbrake Removed), 1: PUSHED(Handbrake Set) Wert am Pin umgekehrt! Actual value inverted! PIN 32, PORT P1.9 |
| STAT_FRONTWISCHER_RSK_EIN | int | Frontwischer Rückstellkontakt Front Wiper Park Position 0: FrontWischer im RSK, 1: FrontWischer nicht im RSK 0: IN PARK POSITION, 1: OUT PARK POSITION PIN 33, PORT P1.10 |
| STAT_HECKWISCHER_RSK_EIN | int | Heckwischer Rückstellkontakt Rear Wiper Park Position 0: HeckWischer im RSK, 1: HeckWischer nicht im RSK 0: IN PARK POSITION, 1: OUT PARK POSITION Wert am Pin umgekehrt! Actual value inverted! PIN 34, PORT P1.11 |
| STAT_PTWAKE_IN_EIN | int | PT-CAN Wake-up Eingang 0: NICHT AKTIV, 1: AKTIV Wert am Pin umgekehrt! Actual value inverted! PIN 35, PORT P1.12 |
| STAT_VR_INT_EIN | int | Voltage Regulator Interrupt Line 0: NICHT AKTIV, 1: AKTIV Wert am Pin umgekehrt! Actual value inverted! Internes Signal der SPEG Not External SPEG Input PIN 36, PORT P1.13 |
| STAT_RX_CAN_DIAG_EIN | int | RX Diagnosis CAN 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 37, PORT P1.14 |
| STAT_RX_CAN_HIGHSPEED_EIN | int | RX High Speed CAN 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 40, PORT P2.1 |
| STAT_RX_DIAG_OBD_EIN | int | RX Diagnosis OBD 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 56, PORT P2.9 |
| STAT_FRONTSCHEIBENHEIZUNG_DIAG_WERT | int | Frontscheibe Heizung Diagnose Front Window Heater Relay Diagnosis 0: OK, 1: FAILURE Wert am Pin umgekehrt! Actual value inverted! PIN 79, PORT P3.10 |
| STAT_RX_CAN_LOWSPEED_EIN | int | RX Low Speed CAN 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 99, PORT P4.5 |
| STAT_KL30G_F2_OFF_DIAG_EIN | int | Bistabiles Relais Off MSA Diagnose Bistable Relay Off MSA Diagnosis 0: OPEN-LOAD or SHORT, OVERTEMP, OVERLOAD (if Load connected and related Output ON) (wenn Last steckt und entsprechender Ausgang EIN) 1: NORMAL PIN 104, PORT P4.10 |
| STAT_KL30G_F2_ON_DIAG_EIN | int | Bistabiles Relais On MSA Diagnose Bistable Relay On MSA Diagnosis 0: OPEN-LOAD or SHORT, OVERTEMP, OVERLOAD (if Load connected and related Output ON) (wenn Last steckt und entsprechender Ausgang EIN) 1: NORMAL PIN 107, PORT P4.13 |
| STAT_SI_DRIVER_RELAIS_SPI_EIN | int | Driver Relays SPI In 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 111, PORT P5.1 |
| STAT_HECKWISCHER_2_DIAG_EIN | int | Heckwischer 2 Diagnose Rear Wiper 2 Diagnosis 0: OPEN-LOAD or SHORT, OVERTEMP, OVERLOAD (if Load connected and related Output ON) (wenn Last steckt und entsprechender Ausgang EIN) 1: NORMAL PIN 113, PORT P5.3 |
| STAT_SI_VR_SPI_EIN | int | Voltage Regulator SPI In 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 117, PORT P5.7 |
| STAT_HECKSCHEIBENHEIZUNG_DIAG_EIN | int | Heckscheibe Heizung Diagnose Rear Window Heater Relay Diagnosis 0: OFF, 1: ON PIN 124, PORT P5.14 |
| STAT_HECKKLAPPE_2_KONTAKT_EIN | int | Heckklappe 2 Kontakt Trunk Lid 2 Contact 0: GESCHLOSSEN, 1: OFFEN 0: CLOSED, 1: OPEN PIN 129, PORT P6.0 |
| STAT_HECKKLAPPE_TASTER_EIN | int | Taster Entriegeln Heckklappe (Interrupt) Trunk Lid Unlock Button 0: KEINE BETÄTIGUNG, TASTER GEDRÜCKT: 1 0: NOT PUSHED, PUSHED: 1 PIN 130, PORT P6.1 |
| STAT_HECKKLAPPE_KONTAKT_EIN | int | Heckklappe Kontakt Trunk Lid Contact (Trunk Ajar Switch) 0: GESCHLOSSEN, 1: OFFEN 0: CLOSED, 1: OPEN PIN 131, PORT P6.2 |
| STAT_ULTRASCHALLSENSOR_EIN | int | Ultraschallsensor Interior Protection System Status (Ultrasonic Sensor) 0: OFF or NOT ACTIVE, 1: ON(1000 ms) or ACTIVE(100 ms.) Wert am Pin umgekehrt! Actual value inverted! PIN 133,PORT P6.4 |
| STAT_DSC_TASTER_EIN | int | ASC/DSC Switch 0: KEINE BETÄTIGUNG, TASTER GEDRÜCKT: 1 0: NOT PUSHED, PUSHED: 1 Wert am Pin umgekehrt! Actual value inverted! PIN 134,PORT P6.5 |
| STAT_WASCHWASSERSTAND_EIN | int | Waschwasserstand Washer Level Sensor 0: Normaler Füllstand, 1: Zu niedriger Füllstand 0: NORMAL, 1: UNDER LEVEL PIN 135,PORT P6.6 |
| STAT_KUEHLMITTELSTAND_EIN | int | Kühlmittelstand Coolant Level Sensor 0: Normaler Füllstand, 1: Zu niedriger Füllstand 0: NORMAL, 1: UNDER LEVEL PIN 136,PORT P6.7 |
| STAT_RX_LIN_UART_EIN | int | RX LIN UART 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 137,PORT P6.8 |
| STAT_KIPPSENSOR_EIN | int | Tilt Sensor Status 0: NICHT AKTIV, 1: AKTIV (500 ms.) Internes Signal der SPEG Wert am Pin umgekehrt! Actual value inverted! PIN 139,PORT P6.10 |
| STAT_SI_EEPROM_SPI_EIN | int | Eeprom SPI In 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 140,PORT P6.11 |
| STAT_KL15_UC_HW_INPUT_EIN | int | KL15 Physical 0: KL15 AUS, 1: KL15 EIN PIN 144,PORT P6.15 |
| STAT_FH_BFTH_ZU_FEEDBACK_EIN | int | NOT IMPLEMENTED YET!!! Fensterheber Hinten Zu, SPI Relais Treiber Feedback Power Window Rear Up, SPI Relay Driver Feedback OFF: 0, ON: 1 SPI_relays_feedback.OUT0 |
| STAT_FH_BFTH_AUF_FEEDBACK_EIN | int | NOT IMPLEMENTED YET!!! Fensterheber Hinten Auf, SPI Relais Treiber Feedback Power Window Rear Down, SPI Relay Driver Feedback OFF: 0, ON: 1 SPI_relays_feedback.OUT1 |
| STAT_FRONTWISCHER_GESCHW_1_FEEDBACK_EIN | int | Frontwischer Geschwindigkeit Relais 1, SPI Relais Treiber Feedback Front Wiper Speed Relay 1, SPI Relay Driver Feedback OFF: 0, ON: 1 SPI_relays_feedback.OUT2 |
| STAT_HECKSCHEIBENHEIZUNG_FEEDBACK_EIN | int | Heckscheibe Heizung Relais, SPI Relais Treiber Feedback Rear Window Heater Relay, SPI Relay Driver Feedback OFF: 0, ON: 1 SPI_relays_feedback.OUT3 |
| STAT_FRONTWISCHER_GESCHW_2_FEEDBACK_EIN | int | Frontwischer Geschwindigkeit Relais 2, SPI Relais Treiber Feedback Front Wiper Speed Relay 2, SPI Relay Driver Feedback 0: OFF, 1: ON SPI_relays_feedback.OUT4 |
| STAT_SIRENE_DWA_FEEDBACK_EIN | int | Status Alarm, SPI Relais Treiber Feedback 0: OFF (no acustic alarm), 1: ON (acustic alarm) SPI_relays_feedback.OUT5 |
| STAT_BISTABILRELAIS_ON_2_FEEDBACK_EIN | int | Bistabiles Relais ON 2, SPI Relais Treiber Feedback Bistable Relay ON 2, SPI Relay Driver Feedback 0: OFF, 1: ON (5 ms &lt; Ton &lt; 1s) Minimum Resting time between Pulses: 1s SPI_relays_feedback.OUT6 |
| STAT_GEBLAESEMOTOR_RELAIS_FEEDBACK_EIN | int | Gebläsemotor Relais, SPI Relais Treiber Feedback Blower Motor Relay, SPI Relay Driver Feedback 0: OFF, 1: ON SPI_relays_feedback.OUT7 |
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
| STAT_ZV_ENTRIEGELN_RELAIS_EIN | int | Zentralverriegelung Entriegelnrelais Central Locking Unlock Relay 0: OFF, 1: ON PIN 1,PORT P0.0 |
| STAT_ZV_VERRIEGELN_RELAIS_EIN | int | Zentralverriegelung Verriegelnrelais Central Locking Lock Relay 0: OFF, 1: ON PIN 2,PORT P0.1 |
| STAT_ZV_ZENTRALSICHERN_RELAIS_EIN | int | Zentralverriegelung Sichernrelais Central Locking Secure Relay 0: OFF, 1: ON PIN 3,PORT P0.2 |
| STAT_ZV_VERRIEGELN_FAHRERTUERE_RELAIS_EIN | int | Zentralverriegelung selektiv Entriegelnrelais Central Locking Lock Driver Relay 0: OFF, 1: ON PIN 4,PORT P0.3 |
| STAT_ZV_AUSGANG_EIN | int | Zentralverriegelung Central Locking Output 0: Aus, 1: Entriegeln, 3: Selektiv Entriegeln, 10: Verriegeln, 11: Entsichern, 14: Sichern 0x00: OFF, 0x01: UNLOCK, 0x03: SELECTIVE, 0x0A: LOCK, 0x0B: UNSECURE, 0x0E: SECURE |
| STAT_HECKWISCHER_EIN | int | Heckwischer Rear Wiper 0: OFF, 1: ON PIN 7,PORT P0.4 |
| STAT_SRA_EIN | int | Head Lamps Washer 0: OFF, 1: ON PIN 9,PORT P0.6 |
| STAT_KLIMAKOMPRESSOR_EIN | int | Climate Compressor 0: OFF, 1: ON PIN 11,PORT P0.8 |
| STAT_DUO_WASCHERPUMPE_VORNE_EIN | int | Front Wascher Pumpe Front Washer Pump 0: OFF, 1: ON PIN 12,PORT P0.9 |
| STAT_DUO_WASCHERPUMPE_HINTEN_EIN | int | Heck Wascher Pumpe Rear Washer Pump 0: OFF, 1: ON PIN 13,PORT P0.10 |
| STAT_DUO_WASCHERPUMPE_AUSGANG_EIN | int | Duo Wascher Pumpe 0 or 3: NO ACTION, 1: FRONT WASHING, 2: REAR WASHING |
| STAT_BISTABILRELAIS_ON_EIN | int | Bistabiles Relais ON Bistable Relay On 0: OFF, 1: ON (5 ms &lt; Ton &lt; 1s) Minimum Resting time between Pulses: 1s Ausruhen der Zeit zwischen Pulses: 1s PIN 14,PORT P0.11 |
| STAT_BISTABILRELAIS_OFF_EIN | int | Bistabiles Relais OFF Bistable Relay OFF 0: OFF, 1: ON (5 ms &lt; Ton &lt; 1s) Minimum Resting time between Pulses: 1s Ausruhen der Zeit zwischen Pulses: 1s PIN 18,PORT P0.13 |
| STAT_SCHLAFEN_STRATEGIE_EIN | int | Dieses Signal wird zum pollen der weckfähigen Eingänge verwendet Immer wenn die Eingänge eingelesen werden, wird dieses Signal gesetzt Für Diagnosezwecke jedoch ungeeignet Sleep Strategy 0: DISABLE, 1: ENABLE PIN 19,PORT P0.14 |
| STAT_KL15_EJB_EIN | int | KL15 for EJB Ignition Relay 0: OFF, 1: ON PIN 20,PORT P0.15 |
| STAT_USIS_EIN | int | Ultraschallsensor Spannungsansteuerung Control to Ultrasonic Sensor Supply 0: LOW, 1: HIGH (12 V im Sensor) PIN 23,PORT P1.2 |
| STAT_GANG_RUCKWAERTS_EIN | int | Rückwärtsgang Reverse Gear Status for EC-Mirror 0: OFF, 1: ON PIN 24,PORT P1.3 |
| STAT_TX_CAN_DIAG_EIN | int | TX Diagnosis CAN 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 38,PORT P1.15 |
| STAT_TX_CAN_HIGHSPEED_EIN | int | TX High Speed CAN 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 41,PORT P2.2 |
| STAT_PORT_AUCSENSOR_EIN | int | AUC Sensor Enable 0: ENABLE, 1: DISABLE PIN 42,PORT P2.3 |
| STAT_TX_DIAG_OBD_EIN | int | TX Diagnosis OBD 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 55,PORT P2.8 |
| STAT_HECKKLAPPE_MOTOR_EIN | int | Heckklappe Freilassung Trunk Lid Release 0: OFF, 1: ON PIN 57,PORT P2.10 |
| STAT_KL30SW_ENABLE_EIN | int | KL30 SW Enable 0: DISABLE, 1: ENABLE PIN 59,PORT P2.12 |
| STAT_HIGHSPEED_CAN_ENABLE_EIN | int | High Speed CAN Enable 0: ENABLE, 1: DISABLE Internes Signal der SPEG Not External SPEG Input PIN 60,PORT P2.13 |
| STAT_DIAG_CAN_ENABLE_EIN | int | Diagnosis CAN Enable 0: ENABLE, 1: DISABLE Internes Signal der SPEG Not External SPEG Input PIN 61,PORT P2.14 |
| STAT_PTWAKE_OUT_EIN | int | PT CAN Wake UP Pulse 0: NICHT AKTIV, 1: AKTIV PIN 62,PORT P2.15 |
| STAT_TX_CAN_LOWSPEED_EIN | int | TX Low Speed CAN 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 98,PORT P4.4 |
| STAT_FRONTSCHEIBENHEIZUNG_EIN | int | Frontscheibe Heizung Relais Front Window Heater Relay 0: OFF, 1: ON PIN 100,PORT P4.6 |
| STAT_ULTRASCHALL_SIRENE_ENABLE_EIN | int | Ultraschall und Sirene Enable Interior Protection/Siren System Enable 0: DISABLE, 1: ENABLE PIN 101,PORT P4.7 |
| STAT_KL30G_F2_OFF_EIN | int | Bistabiles Relais Off MSA Bistable Relay Off MSA 0: OFF, 1: ON (5 ms &lt; Ton &lt; 1s) Minimum Resting time between Pulses: 1s Ausruhen der Zeit zwischen Pulses: 1s PIN 103, PORT P4.9 |
| STAT_KL30G_F2_ON_EIN | int | Bistabiles Relais On MSA Bistable Relay On MSA 0: OFF, 1: ON (5 ms &lt; Ton &lt; 1s) Minimum Resting time between Pulses: 1s Ausruhen der Zeit zwischen Pulses: 1s PIN 105, PORT P4.11 |
| STAT_TANKSENSOREN_ENABLE_EIN | int | FuelTank Sensoren befähigen Fuel Tank Enable 0: DISABLE, 1: ENABLE PIN 106,PORT P4.12 |
| STAT_DRIVER_RELAIS_ENABLE_EIN | int | Driver Relays Enable 0: ENABLE, 1: DISABLE Internes Signal der SPEG PIN 108,PORT P4.14 |
| STAT_SCLK_DRIVER_RELAIS_SPI_EIN | int | Driver Relays SPI Sclk 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 109,PORT P4.15 |
| STAT_SO_DRIVER_RELAIS_SPI_EIN | int | Driver Relays SPI Out 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 110,PORT P5.0 |
| STAT_HECKWISCHER_2_EIN | int | Heckwischer 2 Rear Wiper 2 0: OFF, 1: ON PIN 114, PORT P5.4 |
| STAT_SCLK_VR_SPI_EIN | int | Voltage Regulator SPI Sclk 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 115,PORT P5.5 |
| STAT_SO_VR_SPI_EIN | int | Voltage Regulator SPI Out 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 116,PORT P5.6 |
| STAT_HECKKLAPPE_2_MOTOR_EIN | int | Heckklappe 2 Freilassung Trunk Lid 2 Release 0: OFF, 1: ON PIN 118,PORT P5.8 |
| STAT_LIN_ENABLE_EIN | int | LIN Enable 0: DISABLE, 1: ENABLE Internes Signal der SPEG Not External SPEG Input PIN 122,PORT P5.12 |
| STAT_BISTABILRELAIS_OFF_2_EIN | int | Bistabiles Relais OFF 2 Bistable Relay OFF 2 0: OFF, 1: ON (5 ms &lt; Ton &lt; 1s) Minimum Resting time between Pulses: 1s Ausruhen der Zeit zwischen Pulses: 1s PIN 123,PORT P5.13 |
| STAT_TX_LIN_UART_EIN | int | TX LIN UART 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 138,PORT P6.9 |
| STAT_SO_EEPROM_SPI_EIN | int | Eeprom SPI Out 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 141,PORT P6.12 |
| STAT_SCLK_EEPROM_SPI_EIN | int | Eeprom SPI Clock 0: LOW, 1: HIGH Internes Signal der SPEG Not External SPEG Input PIN 142,PORT P6.13 |
| STAT_EEPROM_ENABLE_EIN | int | Eeprom Enable 0: ENABLE, 1: DISABLE Internes Signal der SPEG Not External SPEG Input PIN 143,PORT P6.14 |
| STAT_FH_BFTH_ZU_EIN | int | NOT IMPLEMENTED YET!!! Fensterheber Hinten Zu Relais Power Window Rear Up 0: OFF, 1: ON SPI_relays_out.OUT0 |
| STAT_FH_BFTH_AUF_EIN | int | NOT IMPLEMENTED YET!!! Fensterheber Hinten Auf Relais Power Window Rear Down 0: OFF, 1: ON SPI_relays_out.OUT1 |
| STAT_FRONTWISCHER_GESCHW_1_EIN | int | Frontwischer Geschwindigkeit Relais 1 Front Wiper Speed Relay 1 0: OFF, 1: ON SPI_relays_out.OUT2 |
| STAT_HECKSCHEIBENHEIZUNG_EIN | int | Heckscheibe Heizung Rear Window Heater OFF: 0, ON: 1 SPI_relays_out.OUT3 |
| STAT_FRONTWISCHER_GESCHW_2_EIN | int | Frontwischer Geschwindigkeit Relais 2 Front Wiper Speed Relay 2 0: OFF, 1: ON SPI_relays_out.OUT4 |
| STAT_SIRENE_DWA_EIN | int | Siren Activation 0: OFF, 1: ON SPI_relays_out.OUT5 |
| STAT_BISTABILRELAIS_ON_2_EIN | int | Bistabiles Relais ON Diagnose Bistable Relay ON Diagnosis 0: OFF, 1: ON (5 ms &lt; Ton &lt; 1s) Minimum Resting time between Pulses: 1s Ausruhen der Zeit zwischen Pulses: 1s SPI_relays_out.OUT6 |
| STAT_GEBLAESEMOTOR_RELAIS_EIN | int | Gebläsemotor Relais Blower Motor Relay 0: OFF, 1: ON SPI_relays_out.OUT7 |
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
| STAT_AUCSENSOR_EIN | int | AUC Sensor Eingang. Pin Wert. PWM Signale 0: NICHT AKTIV, 1: AKTIV (beständig) PIN 17, PORT P0.12 |
| STAT_PWM_PERIOD_AUCSENSOR_WERT | unsigned int | AUC Sensor Eingang Periode. Register wert Wertbereich: 0..0xFFFF(65535) |
| STAT_PERIOD_AUCSENSOR_WERT | real | AUC Sensor Eingang Periode. Physicalisher wert Wertbereich: 0..0xFFFF(65535) 0..131 ms 20 ms (50 Hz PWM): NORMAL [PERIOD]=(20ms/10000)*(STAT_PWM_PERIOD_AUCSENSOR_WERT) |
| STAT_PERIOD_AUCSENSOR_EINH | string | Einheit fuer AUC Sensor Eingang Periode: [Msek] |
| STAT_PWM_DUTY_AUCSENSOR_WERT | unsigned int | AUC Sensor Eingang Tastverhältnis. Register wert AUC Sensor Input Duty-Cycle. Register value Wertbereich: 0..0xFFFF(65535) 0.......:Kurzschluß nach Masse (SHORT-GND) 0xFFFF..:Leitungsunterbrechung (OPEN-LOAD) STAT_PWM_DUTY_AUCSENSOR_WERT &lt;= STAT_PWM_PERIOD_AUCSENSOR_WERT |
| STAT_DUTY_AUCSENSOR_WERT | real | AUC Sensor Eingang Tastverhältnis. Physicalisher wert AUC Sensor Input Duty-Cycle. Physical value Wertbereich: 0..0xFFFF(65535) 0..100 % [Duty]=(STAT_PWM_DUTY_AUCSENSOR_WERT*100)/(STAT_PWM_PERIOD_AUCSENSOR_WERT) |
| STAT_DUTY_AUCSENSOR_EINH | string | Einheit fuer AUC Sensor Eingang Tastverhältnis: [%] |
| STAT_T_ON_AUCSENSOR_WERT | real | AUC Sensor Eingang EIN Zeit Wertbereich: 0..0xFFFF(65535) 0..131 ms [T_ON]=(20ms/10000)*(STAT_PWM_DUTY_AUCSENSOR_WERT) |
| STAT_T_ON_AUCSENSOR_EINH | string | Einheit fuer AUC Sensor Eingang EIN Zeit: [Msek] |
| STAT_SITZHEIZUNG_FA_DIAG_EIN | int | Sitzheizung Fahrer Diagnose.Pin Wert. PWM Signale (25Hz) Seat Heating Driver Diagnosis 0: NICHT AKTIV, 1: AKTIV PIN 21, PORT P1.0 |
| STAT_SITZHEIZUNG_BF_DIAG_EIN | int | Sitzheizung Beifahrer Diagnose.Pin Wert. PWM Signale (25Hz) Seat Heating Passenger Diagnosis 0: NICHT AKTIV, 1: AKTIV PIN 22, PORT P1.1 |
| STAT_ADC_HECKKLAPPE_2_MOTOR_DIAG_WERT | int | Digital Wandler Wert von Heckklappe 2 Freilassung Diagnose Digital converted value from Trunk Lid 2 Release Diagnosis Wertbereich: 0..0x3FF(1023) 0............60 (0x3C)  : OPEN-LOAD	(0.....&lt;0,3V) 61(0x3D).....920(0x398) : OK	 	(0,3V...4,5V) 921(0x399)...1023(0x3FF): SHORT-GND (&gt;4.5V...5V) PIN 72,PORT P3.5 |
| STAT_ADC_BATTERIE_SPANNUNG_WERT | int | Digital Wandler Wert von Batterie Spannung Sensor Digital converted value from Battery Voltage Sensor (HEX) Wertbereich: 0..0x3FF (1023) PIN 73,PORT P3.6 |
| STAT_BATTERIE_SPANNUNG_WERT | real | Batterie Spannung Battery Voltage (Vbat) [V] Wertbereich: 0..18.50 [V] Vbat=(HEX)*100/5530, for Vref=5V PIN 73,PORT P3.6 |
| STAT_BATTERIE_SPANNUNG_EINH | string | Einheit fuer Batterie Spannung: Volt |
| STAT_ADC_FH_HINTEN_SCHALTER_WERT | int | NOT IMPLEMENTED YET!!! Digital Wandler Wert von Fensterheber Hinten Schalter Digital converted value from PowerWindow Rear Button Wertbereich: 0..0x3FF(1023) 143(0x08F)....346(0x15A) : DOWNAUTO(2) 347(0x15B)....571(0x23B) : DOWNMANUAL(1) 572(0x23C)....756(0x2F4) : UPAUTO(4) 757(0x2F5)....951(0x3B7) : UPMANUAL(3) 952(0x3B8)....1023(0x3FF): OFF(0) PIN 74,PORT P3.7 |
| STAT_FH_HINTEN_SCHALTER_EIN | int | NOT IMPLEMENTED YET!!! Fensterheber Fahrer Hinten Schalter 0: Keine Betätigung, 1: Manuell-Öffnen, 2: Maut-Öffnen, 3: Manuell-Schließen, 4: Maut-Schließen PowerWindow Rear-Driver Button 0: OFF, 1: DOWNMANUAL, 2: DOWNAUTO, 3: UPMANUAL, 4: UPAUTO PIN 74,PORT P3.7 |
| STAT_FH_HINTEN_SCHALTER_TEXT | string | NOT IMPLEMENTED YET!!! Fensterheber Hinten Schalter Keine Betätigung:0, Manuell-Öffnen: 1, Maut-Öffnen: 2, Manuell-Schließen:3, Maut-Schließen:4 PowerWindow Rear-Driver Button OFF: 0, DOWNMANUAL: 1, DOWNAUTO: 2, UPMANUAL: 3, UPAUTO: 4 PIN 74,PORT P3.7 |
| STAT_ADC_TANK_LI_FUELLSTAND_WERT | int | Digital Wandler Wert von Fuel Tank Links Digital converted value from Fuel Tank Level Sensor Left Wertbereich: 0..0x3FF(1023) RS= (18,12*(HEX)) / (8388,6*Vbat - 151*(HEX)) PIN 77,PORT P3.8 |
| STAT_TANK_LI_WIDERSTAND_WERT | real | Widerstand Fuel Tank Links Resistance Fuel Tank Level Sensor Left Wertebereich: Gültig: 0..1207 [Ohm], 0xFFFF Signal ungültig 20 Ohm: Full 475 Ohm (1 sensor connected. 40 ltr. Tank): Empty or 295 Ohm (2 sensors connected. 50 ltr. Tank): Empty &lt; 10 Ohm: SHORT-GND &gt; 550 Ohm (1 sensor connected. 40 ltr. Tank): OPEN-LOAD or &gt; 350 Ohm (2 sensors connected. 50 ltr. Tank): OPEN-LOAD PIN 77,PORT P3.8 |
| STAT_TANK_LI_WIDERSTAND_EINH | string | Einheit fuer Widerstand Fuel Tank: Ohm |
| STAT_ADC_TANK_RE_FUELLSTAND_WERT | int | Digital Wandler Wert von Fuel Tank Rechts Digital converted value from Fuel Tank Level Sensor Right Wertbereich: 0..0x3FF(1023) RS= (18,12*(HEX)) / (8388,6*Vbat - 151*(HEX)) PIN 78,PORT P3.9 |
| STAT_TANK_RE_WIDERSTAND_WERT | real | Widerstand Fuel Tank Rechts Resistance Fuel Tank Level Sensor Right Wertebereich: Gültig: 0..1207 [Ohm], 0xFFFF Signal ungültig 20 Ohm: Full 475 Ohm (1 sensor connected. 40 ltr. Tank): Empty or 295 Ohm (2 sensors connected. 50 ltr. Tank): Empty &lt; 10 Ohm: SHORT-GND, OPEN-LOAD &gt; 550 Ohm (1 sensor connected. 40 ltr. Tank): OPEN-LOAD or &gt; 350 Ohm (2 sensors connected. 50 ltr. Tank): OPEN-LOAD PIN 78,PORT P3.9 |
| STAT_TANK_RE_WIDERSTAND_EINH | string | Einheit fuer Widerstand Fuel Tank: Ohm |
| STAT_ADC_HECKBREMSBELAGVERSCHLEISS_WERT | int | Brake Pad Rear Sensor Stage   :Sensor Value :ADC Input (V)		   :ADC Converted Value Stage 0 :  &lt; 5 Ohm    : &lt; 1V				   : &lt; 0xCC (204) Stage 1 :  470 Ohm    : 1V&lt;= x &lt;=4.8V 		   : 0xCC(204)&lt;= x &lt;=0x3D6(982) ± 10%	    (when Vbatt &gt;= 10.5V) 1V&lt;= x &lt;=4V		  	   : 0xCC(204)&lt;= x &lt;=0x332(818) (when Vbatt &lt; 10.5V) Stage 2 :  &gt; 100 kOhm : &gt; 4.8V when Vbatt 10.5V: &gt; 0x3D6(982) &gt; 4V when Vbatt 10.5V  : &gt; 0x332(818) PIN 80,PORT P3.11 |
| STAT_ADC_FRONTBREMSBELAGVERSCHLEISS_WERT | int | Brake Pad Front Sensor Stage   :Sensor Value :ADC Input (V)		   :ADC Converted Value Stage 0 :  &lt; 5 Ohm    : &lt; 1V				   : &lt; 0xCC (204) Stage 1 :  470 Ohm    : 1V&lt;= x &lt;=4.8V 		   : 0xCC(204)&lt;= x &lt;=0x3D6(982) ± 10%	    (when Vbatt &gt;= 10.5V) 1V&lt;= x &lt;=4V		  	   : 0xCC(204)&lt;= x &lt;=0x332(818) (when Vbatt &lt; 10.5V) Stage 2 :  &gt; 100 kOhm : &gt; 4.8V when Vbatt 10.5V: &gt; 0x3D6(982) &gt; 4V when Vbatt 10.5V  : &gt; 0x332(818) PIN 81,PORT P3.12 |
| STAT_ADC_HECKKLAPPE_MOTOR_DIAG_WERT | int | Trunk Lid Release Diagnosis Digital Wandler Wert von Heckklappe Freilassung Diagnose Digital converted value from Trunk Lid Release Diagnosis Wertbereich: 0..0x3FF(1023) 0............60 (0x3C)  : OPEN-LOAD	(0.....&lt;0,3V) 61(0x3D).....920(0x398) : OK	 	(0,3V...4,5V) 921(0x399)...1023(0x3FF): SHORT-GND (&gt;4.5V...5V) PIN 82,PORT P3.13 |
| STAT_ADC_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_DIAG_WERT | int | Digital Wandler Wert von Waschdüsen und Aussenspiegel Heizung Diagnose Digital converted value from Jet Washer and Mirror Heating Diagnosis Wertbereich: 0..0x3FF(1023) 0............60 (0x3C)  : OPEN-LOAD	(0.....&lt;0,3V) 61(0x3D).....920(0x398) : OK	 	(0,3V...4,5V) 921(0x399)...1023(0x3FF): SHORT-GND (&gt;4.5V...5V) PIN 84,PORT P3.15 |
| STAT_DCDC_MSA_EIN | int | MSA DC/DC Converter Diagnose. Pin Wert. PWM Signale 0: NICHT AKTIV, 1: AKTIV PIN 94, PORT P4.0 |
| STAT_PWM_PERIOD_DCDC_MSA_WERT | unsigned int | MSA DC/DC Converter Diagnose Periode. Register wert Wertbereich: 0..0xFFFF(65535) |
| STAT_PERIOD_DCDC_MSA_WERT | real | MSA DC/DC Converter Diagnose Periode. Physicalisher wert Wertbereich: 0..0xFFFF(65535) 0..131 ms 77 ms (13 Hz PWM): OVERTEMPERATURE [PERIOD]=(20ms/10000)*(STAT_PWM_PERIOD_DCDC_MSA_WERT) |
| STAT_PERIOD_DCDC_MSA_EINH | string | Einheit fuer MSA DC/DC Converter Diagnose Periode: [Msek] |
| STAT_PWM_DUTY_DCDC_MSA_WERT | unsigned int | MSA DC/DC Converter Diagnose Tastverhältnis. Register wert MSA DC/DC Converter Diagnose Duty-Cycle. Register value Wertbereich: 0..0xFFFF(65535) 0.......:NORMAL 0xFFFF..:Leitungsunterbrechung (OPEN-LOAD) STAT_PWM_DUTY_DCDC_MSA_WERT &lt;= STAT_PWM_PERIOD_DCDC_MSA_WERT |
| STAT_DUTY_DCDC_MSA_WERT | real | MSA DC/DC Converter Diagnose Tastverhältnis. Physicalisher wert MSA DC/DC Converter Diagnose Duty-Cycle. Physical value Wertbereich: 0..0xFFFF(65535) 0..100 % [Duty]=(STAT_PWM_DUTY_DCDC_MSA_WERT*100)/(STAT_PWM_PERIOD_DCDC_MSA_WERT) |
| STAT_DUTY_DCDC_MSA_EINH | string | Einheit fuer MSA DC/DC Converter Diagnose Tastverhältnis: [%] |
| STAT_T_ON_DCDC_MSA_WERT | real | AUC Sensor Eingang EIN Zeit Wertbereich: 0..0xFFFF(65535) 0..131 ms [T_ON]=(20ms/10000)*(STAT_PWM_DUTY_DCDC_MSA_WERT) |
| STAT_T_ON_DCDC_MSA_EINH | string | Einheit fuer MSA DC/DC Converter Diagnose EIN Zeit: [Msek] |
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
| STAT_SPORT_LED_EIN | int | Sport Led 0: OFF, 1: ON PIN 31,PORT P1.8 |
| STAT_PWM_SPORT_LED_WERT | int | Sport Led Tastverhältnis. Register wert Sport Led Duty-cycle. Register value Wertbereich: 0..0xFFFF(65535) 0...10000 -&gt; 0%...100% &gt;10000    -&gt; 100% PIN 31,PORT P1.8 |
| STAT_DUTY_SPORT_LED_WERT | real | Sport Led Tastverhältnis. Physicalisher wert Sport Led Duty-cycle. Physical value 0...100 % F=80 Hz (fixed) (12.5 ms) [Duty]=(STAT_PWM_SPORT_LED_WERT*100)/10000 |
| STAT_DUTY_SPORT_LED_EINH | string | Einheit fuer DUTY_SPORT_LED: [%] |
| STAT_LED_HEARTBEAT_EIN | int | Led Alarm System for Heartbeat simulation 0: OFF, 1: ON PIN 43,PORT P2.4 |
| STAT_PWM_LED_HEARTBEAT_WERT | int | Duty-Cycle Led Alarm System for Heartbeat simulation PWM 0...100 % F=80 Hz (fixed) (12.5 ms) PIN 43,PORT P2.4 |
| STAT_PWM_LED_HEARTBEAT_EINH | string | Einheit fuer PWM_LED_HEARTBEAT: [%] |
| STAT_LED_DWA_EIN | int | Led Alarm System 0: OFF, 1: ON PIN 44,PORT P2.5 |
| STAT_PWM_LED_DWA_WERT | int | Duty-Cycle Led Alarm Systems PWM 0: OFF, 1: FLASHING (F=0.5 Hz. 50 ms ON), 2: BLINKING (F=2 Hz. 250 ms ON), 3: ON PIN 44,PORT P2.5 |
| STAT_PWM_LED_DWA_TEXT | string | Duty-Cycle Led Alarm Systems PWM OFF: 0, FLASHING: 1 (F=2 Hz. Duty=50%), BLINKING: 2 (Period=2s. Ton=50 ms), ON: 3 |
| STAT_SITZHEIZUNG_FA_EIN | int | Sitzheizung Fahrer Steuer Seat Heating Driver Control 0: LOW, 1: HIGH PIN 45,PORT P2.6 |
| STAT_PWM_SITZHEIZUNG_FA_WERT | int | Duty-Cycle Sitzheizung Fahrer PWM Duty-Cycle SeatHeating Driver Control F=25 Hz (fixed) (40 ms) 0: OFF (100% High Level. 40 ms ON), 1: STATE1 (80%. 32ms ON, 8ms OFF) 2: STATE2 (50%. 20ms ON, 20ms OFF), 3: STATE3 (30%. 12ms ON, 28ms OFF) PIN 45,PORT P2.6 |
| STAT_PWM_SITZHEIZUNG_FA_TEXT | string | Duty-Cycle Sitzheizung Fahrer PWM Duty-Cycle SeatHeating Driver Control OFF: 0 (100% High Level. 40 ms ON), STATE1: 1 (80%. 32ms ON, 8ms OFF) STATE2: 2 (50%. 20ms ON, 20ms OFF), STATE3: 3 (30%. 12ms ON, 28ms OFF) |
| STAT_SITZHEIZUNG_BF_EIN | int | Sitzheizung Beifahrer Steuer Seat Heating Passenger Control 0: LOW, 1: HIGH PIN 46,PORT P2.7 |
| STAT_PWM_SITZHEIZUNG_BF_WERT | int | Duty-Cycle Sitzheizung Beifahrer PWM Duty-Cycle SeatHeating Passenger Control F=25 Hz (fixed) (40 ms) 0: OFF (100% High Level. 40 ms ON), 1: STATE1 (80%. 32ms ON, 8ms OFF) 2: STATE2 (50%. 20ms ON, 20ms OFF), 3: STATE3 (30%. 12ms ON, 28ms OFF) PIN 46,PORT P2.7 |
| STAT_PWM_SITZHEIZUNG_BF_TEXT | string | Duty-Cycle Sitzheizung Beifahrer PWM Duty-Cycle SeatHeating Passenger Control OFF: 0 (100% High Level. 40 ms ON), STATE1: 1 (80%. 32ms ON, 8ms OFF) STATE2: 2 (50%. 20ms ON, 20ms OFF), STATE3: 3 (30%. 12ms ON, 28ms OFF) |
| STAT_WASCHDUESENHEIZUNG_AUSSENSPIEGEL_EIN | int | Waschdüsen und Aussenspiegel Heizung Jet Washer and Mirror Heating F=1 Hz 0: OFF (Temp&gt;5°C without Wiper, Temp&gt;20°C with Wiper) 1: ON (100% High Level Temp &lt;=5°C without Wiper) (100% Temp&lt;=5°C, 75% 5°C&lt;Temp&lt;=10°C, 50% 10°C&lt;Temp&lt;=15°C 25% 15°C&lt;Temp&lt;=20°C with Wiper) Hystheresis +/- 5°C PIN 58,PORT P2.11 |
| STAT_MSA_LED_EIN | int | MSA Led 0: OFF, 1: ON PIN 112,PORT P5.2 |
| STAT_PWM_MSA_LED_WERT | int | MSA Led Tastverhältnis. Register wert MSA Led Duty-cycle. Register value Wertbereich: 0..0xFFFF(65535) 0...10000 -&gt; 0%...100% &gt;10000    -&gt; 100% PIN 112,PORT P5.2 |
| STAT_DUTY_MSA_LED_WERT | real | MSA Led Tastverhältnis. Physicalisher wert MSA Led Duty-cycle. Physical value 0...100 % F=80 Hz (fixed) (12.5 ms) [Duty]=(STAT_PWM_MSA_LED_WERT*100)/10000 |
| STAT_DUTY_MSA_LED_EINH | string | Einheit fuer DUTY_MSA_LED: [%] |
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
| WERT2 | string | table AnalogInputNrTexte WERT nützlich nur fuer AUCSENSOR und DCDC_MSA Tastverhältnis valid only for AUCSENSOR and DCDC_MSA Duty-Cycle |
| ART_WERT | string | "nein"-&gt; ADC register Wert "ja"  -&gt; (PH) Wert default "nein" table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANALOG_INPUT_STATUS | string | ANALOG_INPUT_SET or ERROR_IN_ADDR or ERROR_IN_VALUE |
| ANALOG_INPUT_ADDR | string | ort |
| ANALOG_INPUT_VALUE | string | wert |
| ANALOG_INPUT_CONVERTED_VALUE | string | wert from SPEG (ADC oder (PH)) |
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

<a id="job-steuern-beenden"></a>
### STEUERN_BEENDEN

Kontrolle an SPEG zurueckgeben KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Input $02 Digitale Output $03 Analoge Input $04 Analoge Output $00 ReturnControToECU

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

<a id="job-status-var-can-general"></a>
### _STATUS_VAR_CAN_GENERAL

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $00 GENERAL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMMEN_R_EIN | int | Klemmen R 0: OFF, 1: ON |
| STAT_KLEMMEN_15_EIN | int | Klemmen 15 0: OFF, 1: ON |
| STAT_KLEMMEN_50_EIN | int | Klemmen 50 0: OFF, 1: ON |
| STAT_KLEMMEN_61_EIN | int | Klemmen 61 0: OFF, 1: START, 2: GO |
| STAT_KLEMMEN_58G_EIN | int | Klemmen 61 0: OFF, 1: START, 2: GO |
| STAT_GESCHWINDIGKEIT_FAHRZEUG_BUS_WERT | unsigned int | Value in Bus for Vehicle Speed (HEX) PTCAN0x1A0_BYTE0_BYTE1 Zykluszeit: ttyp = 100ms (tmin = 95ms, tmax = 105ms) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich: 0..3200 (HEX) Sender: PT-CAN DSC_Modul |
| STAT_GESCHWINDIGKEIT_FAHRZEUG_WERT | real | Vehicle Speed (VS)[Km/h] Wertebereich: 0..320 [km/h] (PH) = 0,1 * (HEX)  [km/h] |
| STAT_GESCHWINDIGKEIT_FAHRZEUG_EINH | string | Einheit fuer Vehicle Speed: Km/h |
| STAT_AUSSENTEMPERATUR_BUS_WERT | int | Value in Bus for Exterior Temperature (HEX) KCAN0x2CA_BYTE0 Zykluszeit: ttyp = 1s (tmin = 0,9s, tmax = 1,1s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich: 0&lt;-&gt;255 Sender: K_CAN Kombi |
| STAT_AUSSENTEMPERATUR_WERT | real | Exterior Temperature (T) [°C] Wertebereich:0..255 (HEX) (T)= 0,5 * (HEX)-40 [°C], -40..+85 [°C] |
| STAT_AUSSENTEMPERATUR_EINH | string | Einheit fuer Exterior Temperature: °C |
| STAT_RELATIVZEIT_WERT | unsigned long | Relative Time [s] KCAN0x328_BYTE0_BYTE1_BYTE2_BYTE3 Zykluszeit: ttyp = 1s (tmin = 0,9s, tmax = 1,1s) Aktivbedingung = BUS_AKTIV Startbedingung = BUS_AKTIV_ON, Stopbedingung = BUS_AKTIV_OFF Wertebereich:0..0xFFFFFFFF&lt;-&gt;0..4.294.967.294 [s] (136,9 jahres) Sender: K_CAN Kombi |
| STAT_RELATIVZEIT_EINH | string | Einheit fuer Relative Time: Sek(s) |
| STAT_KILOMETERSTAND_WERT | unsigned long | Kilometre [Km] KCAN0x330_BYTE0_BYTE1_BYTE2 Zykluszeit: ttyp = 10s (tmin = 9s, tmax = 11s) Aktivbedingung = KL_R Startbedingung = KL_R_ON, Stopbedingung = KL_R_OFF Wertebereich:0..0xFFFFFF&lt;-&gt;0..16.777.214 [Km] Sender: K_CAN Kombi |
| STAT_KILOMETERSTAND_EINH | string | Einheit fuer Kilometre: Km |
| STAT_RUECKWAERTSGANG_EIN | int | Manual Reverse Gear |
| STAT_GETRIEBEDATEN_EIN | int | Automatic Reverse Gear (Gear System Data) |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-wws"></a>
### _STATUS_VAR_CAN_WWS

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $01 WWS (Wiper-Washer System)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FRONTWISCHER_POTI_EIN | int | -- |
| STAT_FRONTWISCHER_BEFEHL_EIN | int | -- |
| STAT_FRONTWASCHERPUMPE_BEFEHL_EIN | int | -- |
| STAT_HECKWISCHER_BEFEHL_EIN | int | -- |
| STAT_HECKWASCHERPUMPE_BEFEHL_EIN | int | -- |
| STAT_FRONTWISCHERNOTLAUF_WERT | int | -- |
| STAT_CONFIG_RLS_CKM_IND_WERT | int | -- |
| STAT_ST_RLS_CKM_SEND_WERT | int | -- |
| STAT_ST_RLS_THRV_LP_CKM_WERT | int | -- |
| STAT_SU_RLS_THRV_LP_CKM_WERT | int | -- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-zvs"></a>
### _STATUS_VAR_CAN_ZVS

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $02 ZVS (Central Locking System)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZV_BEFEHL_WERT | int | -- |
| STAT_ZV_STATUS_FAT_WERT | int | -- |
| STAT_ZV_STATUS_BFT_WERT | int | -- |
| STAT_ZV_STATUS_FATH_WERT | int | -- |
| STAT_ZV_STATUS_BFTH_WERT | int |  |
| STAT_TUERKONTAKT_FAT_EIN | int | -- |
| STAT_TUERKONTAKT_BFT_EIN | int | -- |
| STAT_TUERKONTAKT_FATH_EIN | int | -- |
| STAT_TUERKONTAKT_SICHERN_FAT_EIN | int | -- |
| STAT_TUERKONTAKT_BFTH_EIN | int | -- |
| STAT_CRASH_STATUS_WERT | int | -- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-dwa"></a>
### _STATUS_VAR_CAN_DWA

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $03 DWA (Anti-Theft Alarm System)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_ALARM_WERT | int | -- |
| STAT_DWA_RCPT_WERT | int | -- |
| STAT_DWA_PANIC_WERT | int | -- |
| STAT_CONFIG_DWA_CKM_IND_WERT | int | -- |
| STAT_ST_DWA_CKM_SEND_WERT | int | -- |
| STAT_ST_DWA_ACUS_ARM_SMPL_CKM_WERT | int | -- |
| STAT_ST_DWA_OPT_ARM_SMPL_CKM_WERT | int | -- |
| STAT_ST_DWA_ACUS_DSARM_CKM_WERT | int | -- |
| STAT_ST_DWA_OPT_DSARM_CKM_WERT | int |  |
| STAT_SU_DWA_ACUS_ARM_SMPL_CKM_WERT | int | -- |
| STAT_SU_DWA_OPT_ARM_SMPL_CKM_WERT | int | -- |
| STAT_SU_DWA_ACUS_DSARM_CKM_WERT | int |  |
| STAT_SU_DWA_OPT_DSARM_CKM_WERT | int | -- |
| STAT_REMOTE_UNLOCK_WERT | int | -- |
| STAT_REMOTE_LOCK_WERT | int | -- |
| STAT_KLP_STATUS_CONTACT_BONET_WERT | int |  |
| STAT_ZHK_BEFEHL_WERT | int | -- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-ph-kombi"></a>
### _STATUS_VAR_CAN_PH_KOMBI

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $04 PH_KOMBI (Peripherics Kombi)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KUEHLMITTELSTAND_WERT | int | -- |
| STAT_WASCHWASSERSTAND_WERT | int | -- |
| STAT_HB_ON_WERT | int | -- |
| STAT_TANK_FA_WIDERSTAND_WERT | int | -- |
| STAT_TANK_BF_WIDERSTAND_WERT | int | -- |
| STAT_TAS_CONTACT_WERT | int | -- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-ph-misc"></a>
### _STATUS_VAR_CAN_PH_MISC

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $05 PH_MISC (Peripherics Miscelaneous)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DSC_ON_WERT | int | -- |
| STAT_MSA_STATUS_WERT | int | -- |
| STAT_MSA_TASTER_WERT | int | -- |
| STAT_BISTABILRELAIS_OFF_BEFEHL_WERT | int | -- |
| STAT_BISTABILRELAIS_RESET_BEFEHL_WERT | int | -- |
| STAT_BISTABILRELAIS_LIGHSTS_ON_WERT | int | -- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-ach"></a>
### _STATUS_VAR_CAN_ACH

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $07 ACH (Air Conditioning / Heating)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FRONTSCHEIBENHEIZUNG_BEFEHL_WERT | int | -- |
| STAT_FRONTSCHEIBENHEIZUNG_0_LIMIT_WERT | int | -- |
| STAT_HECKSCHEIBENHEIZUNG_BEFEHL_WERT | int | -- |
| STAT_HECKSCHEIBENHEIZUNG_0_LIMIT_WERT | int | -- |
| STAT_SITZHEIZUNG_FA_BEFEHL_EIN | int | -- |
| STAT_SITZHEIZUNG_BF_BEFEHL_EIN | int | -- |
| STAT_SITZHEIZUNG_FA_STATUS_EIN | int | -- |
| STAT_SITZHEIZUNG_BF_STATUS_EIN | int | -- |
| STAT_SH_50_LIMIT_WERT | int | -- |
| STAT_SH_0_LIMIT_WERT | int | -- |
| STAT_GEBLASEMOTOR_BEFEHL_WERT | int | -- |
| STAT_ACR_BEFEHL_WERT | int | -- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-can-pia"></a>
### _STATUS_VAR_CAN_PIA

Auslesen der Stati von den Internen CAN Nachrichten Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $05 Internal Variables CAN Nachrichten $01 ReportCurrentState $09 PIA (Personalization, Individualization, Adaption)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NO_KEY_PRSL_IMME_EIN | int | -- |
| STAT_NO_KEY_PRSL_EIN | int | -- |
| STAT_STAT_FUNKSCHLUESSEL_ANFRAGE_EIN | int | -- |
| STAT_STAT_FUNKSCHLUESSEL_IND_EIN | int | -- |
| STAT_PIA_INTERNER_USER | int | Im RAM gespeicherte aktuell gültige Profil |
| STAT_PIA_ALTER_INTERNER_USER | int | Im RAM gespeicherte alt gültige Profil |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-general"></a>
### _STATUS_VAR_IAP_GENERAL

Auslesen der Stati von den Internen Application Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables Application $01 ReportCurrentState $00 GENERAL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SAL_IS_LOADED_EIN | int | -- |
| STAT_VEHICLE_SPEED_CLASS_EIN | int | -- |
| STAT_BATTERY_VOLTAGE_CLASS_EIN | int | -- |
| STAT_SLEEP_ECU_EIN | int | -- |
| STAT_B30_AWAKE_TIME_EIN | int | -- |
| STAT_BUS_STATUS_EIN | int | -- |
| STAT_DNMT_EIN | int | -- |
| STAT_NMID_0_EIN | int | -- |
| STAT_NMID_1_EIN | int | -- |
| STAT_KEY_POSITION_EIN | int | -- |
| STAT_SM_FA_PRESENT_EIN | int | -- |
| STAT_SM_BF_PRESENT_EIN | int | -- |
| STAT_SH_CONFIG_ACTIVE_EIN | int | -- |
| STAT_ZV_REPETITION_BLOCK_EIN | int | -- |
| STAT_ZHK_REPETITION_BLOCK_EIN | int | -- |
| STAT_ST_ENERGIE_SPAR_MODE_EIN | int | -- |
| STAT_ST_REAR_WINDOW_HEATER_CAN_EIN | int | -- |
| STAT_ST_SH_PASS_CAN_EIN | int | -- |
| STAT_ST_SH_DRV_CAN_EIN | int | -- |
| STAT_INIT_DELAY_DTCS_ELAPSED_EIN | int | -- |
| STAT_VBAT_IN_RANGE_FOR_NOT_CAN_DTCS_EIN | int | -- |
| STAT_VBAT_IN_RANGE_FOR_CAN_DTCS_EIN | int | -- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-wws"></a>
### _STATUS_VAR_IAP_WWS

Auslesen der Stati von den Internen Application Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $06 Internal Variables Application $01 ReportCurrentState $01 WWS (Wiper-Washer System)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FWI_OUTPUT_EIN | int | -- |
| STAT_FWI_IS_BLOCKED_EIN | int | -- |
| STAT_FWI_IN_PARK_EIN | int | -- |
| STAT_FWA_LONG_ACTIVATION_EIN | int | -- |
| STAT_ST_FRONT_PARK_EIN | int | -- |
| STAT_RWI_IS_BLOCKED_EIN | int | -- |
| STAT_RWI_IN_PARK_EIN | int | -- |
| STAT_RWA_LONG_ACTIVATION_EIN | int | -- |
| STAT_ST_REAR_PARK_EIN | int | -- |
| STAT_LIN_BUS_EIN | int | -- |
| STAT_ST_RLS_EIN | int | -- |
| STAT_RLS_CLEAR_DTCS_COUNTER_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_00_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_01_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_02_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_03_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_04_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_05_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_06_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RESP_BYTE_07_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RQ_BYTE_00_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RQ_BYTE_01_LIN_EIN | int |  |
| STAT_EOL_TST_RLS_RQ_BYTE_02_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RQ_BYTE_03_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RQ_BYTE_04_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RQ_BYTE_05_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RQ_BYTE_06_LIN_EIN | int | -- |
| STAT_EOL_TST_RLS_RQ_BYTE_07_LIN_EIN | int | -- |
| STAT_RLS_PREVIOUS_SUBSERVICE_EIN | int | -- |
| STAT_RLS_FRAME_SIZE_EIN | int | -- |
| STAT_RLS_SID_STATUS_EIN | int | -- |
| STAT_RLS_SID_OCCUPIED_EIN | int | -- |
| STAT_RLS_PENDING_RESPONSE_EIN | int | -- |
| STAT_RLS_REPEAT_REQUEST_EIN | int | -- |
| STAT_LIN_RSID_CF_COMPLETED_EIN | int | -- |
| STAT_RLS_SID_FAILED_EIN | int | -- |
| STAT_RLS_SID_RECEIVED_EIN | int | -- |
| STAT_INTERMITTENT_TIME_LIN_EIN | long | -- |
| STAT_LIN_BUS_SLEEP_EIN | int | -- |
| STAT_ST_RLS_THRV_PIA_UPDATED_EIN | int | -- |
| STAT_STATUS_RAINSENSOR_LIN_EIN | int | -- |
| STAT_ACTIVATE_WIPER_SPRAY_NOZZLE_EIN | int | -- |
| STAT_SPEED_WIPER_LIN_EIN | int | -- |
| STAT_TIME | string | Date&Time |
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
| STAT_DATENSATZ_2 | string | Daten des zweiten Einschlafverhinderers |
| STAT_VERURSACHER_2 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_2 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_2 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_2 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_3 | string | Daten des dritten Einschlafverhinderers |
| STAT_VERURSACHER_3 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_3 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_3 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_3 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_4 | string | Daten des vierten Einschlafverhinderers |
| STAT_VERURSACHER_4 | int | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_4 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_4 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_4 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_5 | string | Daten des fünften Einschlafverhinderers |
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

<a id="job-status-lear-versions"></a>
### _STATUS_LEAR_VERSIONS

Reading of the internal LEAR Application Software Version Lesen der internen Versionsnummer der Applikationssoftware KWP2000: $21 ReadDataByLocalIdentifier $70 RecordLocalId

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSION_APPL_SOFTWARE_LEAR | string | Versionsnummer (Application-Software) Results in DEC |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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

<a id="job-status-lesen-wischertaster"></a>
### STATUS_LESEN_WISCHERTASTER

Auslesen des Wischertasterstatus KWP2000: 0x23 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RESULT_DATA | binary | Rändelradstellung data |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sg-init"></a>
### SG_INIT

RLS_Initialisation KWP2000: $3D $00 $08 $20 $00 $01 $FF WriteMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-rls-ident"></a>
### RLS_IDENT

KWP2000:  1. READ LEAR VERSION $21 $70 ReadDataByLocalIdentifier 2. LEAR VERSION &lt;V6.2.0  -&gt; $22 $16 $01 ReadDataByLocalIdentifier READ VERSION &gt;=V6.2.0 -&gt; $21 $A3 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| RLS_ID_BMW_NR | string | BMW-Teilenummer |
| RLS_ID_HW_NR | string | BMW-Hardware-Versionsindex |
| RLS_ID_COD_INDEX | int | Codier-Index |
| RLS_ID_DIAG_INDEX | int | Diagnose-Index |
| RLS_ID_VAR_INDEX | int | Varianten-Index |
| RLS_ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| RLS_ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| RLS_ID_DATUM_TAG | int | Herstelldatum (Tag) |
| RLS_ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| RLS_ID_LIEF_NR | int | Lieferanten-Nummer |
| RLS_ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| RLS_ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| RLS_ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| RLS_ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| RLS_ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| RLS_ID_SG_ADR | long | Steuergeraeteadresse bzw. LIN Master Steuergeraeteadresse |
| RLS_ID_LIN_SLAVE_ADR | long | LIN Slave Steuergeraeteadresse |
| RLS_ID_EWS_SS | int | Identifikation EWS-Schnittstelle Nur fuer DS2-Bordnetz benoetigt Fuer EWS-DME/DDE Abgleich |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-rls"></a>
### STATUS_LESEN_RLS

KWP2000: $30 $5501 InputOutputControlByLocalID

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STROM0_WERT | real | Strom Meßstrecke 0 Bereich: V=0,1,2: 10 bis 254 V=3    : 10 bis 200 |
| STAT_STROM0_EINH | string | Einheit: Digits |
| STAT_STROM1_WERT | real | Strom Meßstrecke 1 Bereich: V=0,1,2: 10 bis 254 V=3    : 10 bis 200 |
| STAT_STROM1_EINH | string | Einheit: Digits |
| STAT_STROM2_WERT | real | Strom Meßstrecke 2 Bereich: V=0,1,2: 10 bis 254 V=3    : 10 bis 200 |
| STAT_STROM2_EINH | string | Einheit: Digits |
| STAT_STROM3_WERT | real | Strom Meßstrecke 3 Bereich: V=0,1,2: 10 bis 254 V=3    : 10 bis 200 |
| STAT_STROM3_EINH | string | Einheit: Digits |
| STAT_VERSTAERKUNGSFAKTOR_WERT | real | Grundverstärkungsfaktor Verstärkungsbereiche 0 (kleine Verstärkung) bis 3 (große Verstärkung) aufsteigend |
| STAT_VERSTAERKUNGSFAKTOR_EINH | string | Einheit: Digits |
| STAT_FRONTLICHTWERT_WERT | real | ungefilterter Frontlichtwert Bereich: 0 bis 255 |
| STAT_FRONTLICHTWERT_EINH | string | Einheit: Digits |
| STAT_UMGEBUNGSLICHTWERT_WERT | real | ungefilterter Umgebungslichtwert Bereich: 0 bis 255 |
| STAT_UMGEBUNGSLICHTWERT_EINH | string | Einheit: Digits |
| STAT_HEIZUNGSTEMPERATUR_WERT | real | Heizungstemperatur Bereich: 0 bis 255 |
| STAT_HEIZUNGSTEMPERATUR_EINH | string | Einheit: Digits |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen-rls"></a>
### C_AEI_LESEN_RLS

RLS Aenderungsindex der Codierdaten lesen KWP2000: $21 $A0 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen-rls"></a>
### C_FG_LESEN_RLS

RLS Fahrgestellnummer lesen KWP2000: $21 $A1 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben-rls"></a>
### C_AEI_SCHREIBEN_RLS

KWP2000: $3B $A0 WriteDataByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANSDERUNGSINDEX | string | 2 DATA BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben-rls"></a>
### C_FG_SCHREIBEN_RLS

KWP2000: $3B $A1 WriteDataByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRGESTELLNR | string | 18 data bytes supported by RLS only 7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag-rls"></a>
### C_AEI_AUFTRAG_RLS

KWP2000: $3B $A0 WriteDataByLocalIdentifier and $21 $A0 ReadDataByLocalIdentifier ANSDERUNGSINDEX examples: 31 32 (12) 61 62 (ab)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANSDERUNGSINDEX | string | 2 DATA BYTES Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag-rls"></a>
### C_FG_AUFTRAG_RLS

KWP2000: $3B $A1 WriteDataByLocalIdentifier and $21 $A1 ReadDataByLocalIdentifier FAHRGESTELLNR examples: 31 32 33 34 35 36 37 (1234567) 61 62 63 64 65 66 67(abcdefg)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRGESTELLNR | string | 18 data bytes supported by RLS only 7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

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
| OSEK_TASK_Cyclic_4 | unsigned int | time consumption in ms |
| OSEK_TASK_Cyclic_10 | unsigned int | time consumption in ms |
| OSEK_TASK_Cyclic_20 | unsigned int | time consumption in ms |
| OSEK_TASK_Cyclic_50 | unsigned int | time consumption in ms |
| OSEK_TASK_Cyclic_15 | unsigned int | time consumption in ms |
| OSEK_TASK_DTC_Wait_Enable | unsigned int | time consumption in ms |
| OSEK_TASK_GwCycTask | unsigned int | time consumption in ms |
| OSEK_TASK_ReceiveTask | unsigned int | time consumption in ms |
| OSEK_TASK_SendTask | unsigned int | time consumption in ms |
| OSEK_TASK_DiagnoseTask | unsigned int | time consumption in ms |
| OSEK_TASK_GwCycDiagTask | unsigned int | time consumption in ms |
| OSEK_TASK_KLineMsgReceiveTask | unsigned int | time consumption in ms |
| OSEK_TASK_DCanMsgReceiveTask | unsigned int | time consumption in ms |
| OSEK_TASK_Cyclic_1 | unsigned int | time consumption in ms |
| OSEK_TASK_TpCfTask_0 | unsigned int | time consumption in ms |
| OSEK_TASK_TpCfTask_1 | unsigned int | time consumption in ms |
| OSEK_TASK_TpCfTask_2 | unsigned int | time consumption in ms |
| OSEK_TASK_GwDCanTimeoutTask | unsigned int | time consumption in ms |
| SLICE | unsigned int | time consumption in ms |
| INTERRUPTS_COUNTER | unsigned int | How many interrupts |
| INTERRUPTS | unsigned int | time consumption in ms |
| MAX_CPU_LOAD | unsigned int | max cpu consumption in % |
| AVG_CPU_LOAD | unsigned int | avg cpu consumption in % |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-intern"></a>
### STATUS_DWA_INTERN

Readout of the application status of the DWA KWP2000: $21 ReadDataByLocalIdentifier $A2 identifier of the DWA_STS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DWA_INTERN | int | dwa application status table DWA_Status_Tabelle-STAT_DWA_NUMBER |
| STAT_DWA_INTERN_TEXT | string | dwa application status table DWA_Status_Tabelle-&gt;STAT_DWA_NAME |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-wakeup-reason"></a>
### _READ_WAKEUP_REASON

Returns the last wake-up reason KWP2000: $21 ReadDataByLocalIdentifier $71 RecordLocalId

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKEUP_REASON | string | Last wake-up reason table WakeupReason_table-&gt;WAKEUP_REASON_NAME |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-irs-selftest"></a>
### STEUERN_DWA_IRS_SELFTEST

Self Test of the INRS DWA KWP2000: $31 StartRoutineByLocalIdentifier $04 SelfTest $00 INRS DWA Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-ng-selftest"></a>
### STEUERN_DWA_NG_SELFTEST

Self Test of the NG DWA KWP2000: $31 StartRoutineByLocalIdentifier $04 SelfTest $01 NG DWA Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-alarmtrigger"></a>
### STATUS_ALARMTRIGGER

Return the status of every trigger of the DWA KWP2000: $21 ReadDataByLocalIdentifier $A4 identifier of the STATUS_ALARMTRIGGER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DRIVER_DOOR_CONTACT | string | Status of the driver's door contact GESCHLOSSEN, OFFEN CLOSED, OPEN |
| STAT_PASSENGER_DOOR_CONTACT | string | Status of the passenger's door contact GESCHLOSSEN, OFFEN CLOSED, OPEN |
| STAT_REAR_DRIVER_DOOR_CONTACT | string | Status of the rear driver's door contact GESCHLOSSEN, OFFEN CLOSED, OPEN |
| STAT_REAR_PASSENGER_DOOR_CONTACT | string | Status of the rear passenger's door contact GESCHLOSSEN, OFFEN CLOSED, OPEN |
| STAT_TRUNK_CONTACT | string | Status of the trunk contact GESCHLOSSEN, OFFEN, NICHT VERFÜGBAR CLOSED, OPEN, NOT AVAILABLE |
| STAT_BONNET_CONTACT | string | Status of the bonnet contact GESCHLOSSEN, OFFEN, NICHT VERFÜGBAR CLOSED, OPEN, NOT AVAILABLE |
| STAT_USIS_SENSOR_STATUS | string | Status of the USIS sensor input NICHT GESCHÄRFT, GESCHÄRFT, SENSOR OHNE ACKNOWLEDGE PULS, ALARMAUSLÖSER DISARMED, ARMED, NOT_FITTED, TRIGGER |
| STAT_TILT_SENSOR_STATUS | string | Status of the TILT sensor input NICHT GESCHÄRFT, GESCHÄRFT, SENSOR OHNE ACKNOWLEDGE PULS, ALARMAUSLÖSER DISARMED, ARMED, NOT_FITTED, TRIGGER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (12 × 2)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (43 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [HORTTEXTE](#table-horttexte) (9 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (1 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (26 × 9)
- [IORTTEXTE](#table-iorttexte) (11 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (2 × 9)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [EEPROM_INIT_TABLE](#table-eeprom-init-table) (4 × 3)
- [VARIANT_TABLE](#table-variant-table) (4 × 3)
- [DWA_STATUS_TABELLE](#table-dwa-status-tabelle) (15 × 2)
- [WAKEUPREASON_TABLE](#table-wakeupreason-table) (8 × 2)
- [DWA_HISTORIENSPEICHER_TRIGGERS](#table-dwa-historienspeicher-triggers) (1 × 17)
- [DWA_HISTORIENSPEICHER_DATE](#table-dwa-historienspeicher-date) (1 × 5)
- [DWA_HISTORIENSPEICHER_WINDOWS](#table-dwa-historienspeicher-windows) (1 × 5)
- [POWERWINDOWDRIVER_STATUS](#table-powerwindowdriver-status) (5 × 2)
- [POWERWINDOWPASSENGER_STATUS](#table-powerwindowpassenger-status) (5 × 2)
- [SHD_STATUS](#table-shd-status) (5 × 2)
- [SHD_TILT_STATUS](#table-shd-tilt-status) (5 × 2)
- [FUNKTIONALEADRESSE_LEAR](#table-funktionaleadresse-lear) (7 × 3)
- [DIGITALINPUTNRTEXTE](#table-digitalinputnrtexte) (30 × 4)
- [DIGITALOUTPUTNRTEXTE](#table-digitaloutputnrtexte) (37 × 4)
- [ANALOGINPUTNRTEXTE](#table-analoginputnrtexte) (14 × 4)
- [ANALOGOUTPUTNRTEXTE](#table-analogoutputnrtexte) (8 × 4)

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

<a id="table-harttexte"></a>
### HARTTEXTE

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 12 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0100 | Batteriesensor |
| 0x0200 | Elektrische Wasserpumpe |
| 0x0300 | Generator 1 |
| 0x0350 | Generator 2 |
| 0x0400 | Schaltzentrum Lenksäule |
| 0x0500 | DSC Sensor-Cluster |
| 0x0600 | Nahbereichsradarsensor links |
| 0x0700 | Nahbereichsradarsensor rechts |
| 0x0800 | Funkempfänger |
| 0x0900 | Elektrische Lenksäulenverriegelung |
| 0x0A00 | Regen- Lichtsensor |
| 0xFFFF | unbekannter Verbauort |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

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

Dimensions: 43 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA128 | HARDWAREFEHLER_REGENSENSOR |
| 0xA129 | KEINE_OPTISCHE_INITIALISIERUNG_MÖGLICH |
| 0xA12A | ÜBERTEMPERATUR |
| 0xA12B | ÜBERSPANNUNG |
| 0xA12D | HARDWAREFEHLER_LICHTSENSOR |
| 0xA12E | KALIBRIERUNGSFEHLER_LICHTSENSOR |
| 0xA6C9 | WISCHER_FRONT_BLOCKIERT |
| 0xA6CA | WISCHER_STUFE_1_RELAIS |
| 0xA6CB | WISCHER_STUFE_2_RELAIS |
| 0xA6CD | WISCHER_HECK_BLOCKIERT |
| 0xA6CF | AUC_SENSOR |
| 0xA6DF | AUSSENSPIEGEL_HEIZUNG |
| 0xA6E0 | SITZHEIZUNG_FAHRER |
| 0xA6E1 | SITZHEIZUNG_BEIFAHRER |
| 0xA6E2 | ZV_ANTRIEB_HECKKLAPPE |
| 0xA6E4 | SENSOR_TANK_LINKS |
| 0xA6E5 | SENSOR_TANK_RECHTS |
| 0xA6E7 | Energiesparmode aktiv |
| 0xA730 | BISTABILES_RELAIS_1 |
| 0xA733 | DC_DC_WANDLER |
| 0xA868 | FRONTSCHEIBENHEIZUNG_RELAIS |
| 0xA869 | K_CAN_ID220_FRONTSCHHEIZUNG_UNGUELT |
| 0xA86A | FH_HINTEN_RELAIS |
| 0xA86B | SCHALTER_FH_HINTEN |
| 0xA86D | HECKSCHEIBENHEIZUNG_RELAIS |
| 0xA86E | UNTERSPANNUNG |
| 0xA86F | UEBERSPANNUNG |
| 0xA870 | K_CAN_ID220_FRONTSCHHEIZUNG_TIMEOUT |
| 0xC904 | K_CAN_LOW_LEITUNG |
| 0xC905 | K_CAN_HIGH_LEITUNG |
| 0xC907 | K_CAN_KOMMUNIKATION |
| 0xC90B | PT_CAN_KOMMUNIKATION |
| 0xC910 | PT_CAN_ID1B6_WAERMESTROM_MOTOR_TIMEOUT |
| 0xC911 | PT_CAN_ID1B6_WAERMESTROM_MOTOR_UNGUELTIG |
| 0xC912 | K_CAN_ID246_HECKSCHHEIZUNG_UNGUELT |
| 0xC913 | LIN_KOMMUNIKATION |
| 0xC914 | PT_CAN_ID2A6_BEDIENUNG_WISCHER_TIMEOUT |
| 0xC918 | K_CAN_ID1E7_SITHEIZUNG_FA_UNGUELT |
| 0xC91A | K_CAN_ID1E7_SITHEIZUNG_BF_UNGUELT |
| 0xC91E | K_CAN_ID_130_KLEMMENSTATUS_TIMEOUT  |
| 0xC91F | K_CAN_ID2C0_LCD-LEUCHTD_TIMEOUT |
| 0xC920 | K_CAN_ID2C0_LCD-LEUCHTD_UNGUELTIG |
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
| 0x02 | BatterieSpannung | volt | high | unsigned int | - | 1850 | 102400 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9315 | ALARM_INNENRAUMSENSOR |
| 0x9317 | ALARM_KLAPPENKONTAKT_MOTORHAUBE |
| 0x9318 | ALARM_KLAPPENKONTAKT_KOFFERRAUM |
| 0x9319 | ALARM_KLAPPENKONTAKT_FAHRERTUER_VORNE |
| 0x931A | ALARM_KLAPPENKONTAKT_BEIFAHRERTUER_VORNE |
| 0x931B | ALARM_KLAPPENKONTAKT_CLUBDOOR |
| 0x9324 | PANIKALARM |
| 0x9328 | ALARM_NEIGUNGSSENSOR |
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
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | DWA_Historienspeicher_Triggers | DWA_Historienspeicher_Date | DWA_Historienspeicher_Windows | 0x19 |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 26 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Status Türkontakt Fahrer vorne | 0/1 | low | 0x0001 | - | 1 | 1 | 0 |
| 0x02 | Status Türkontakt Fahrer hinten | 0/1 | low | 0x0002 | - | 1 | 1 | 0 |
| 0x03 | Status Türkontakt Beifahrer vorne | 0/1 | low | 0x0004 | - | 1 | 1 | 0 |
| 0x04 | Status Türkontakt Beifahrer hinten | 0/1 | low | 0x0008 | - | 1 | 1 | 0 |
| 0x05 | Status Motorhaubenkontakt | 0/1 | low | 0x0010 | - | 1 | 1 | 0 |
| 0x06 | Status Heckklappeenkontakt | 0/1 | low | 0x0020 | - | 1 | 1 | 0 |
| 0x07 | Status Ultraschallsensor (USIS) | 0/1 | low | 0x0040 | - | 1 | 1 | 0 |
| 0x08 | Status Neigungsgeber | 0/1 | low | 0x0080 | - | 1 | 1 | 0 |
| 0x09 | Unbekannter Alarmtrigger 1 | 0/1 | low | 0x0100 | - | 1 | 1 | 0 |
| 0x0A | Unbekannter Alarmtrigger 2 | 0/1 | low | 0x0200 | - | 1 | 1 | 0 |
| 0x0B | Unbekannter Alarmtrigger 3 | 0/1 | low | 0x0400 | - | 1 | 1 | 0 |
| 0x0C | Unbekannter Alarmtrigger 4 | 0/1 | low | 0x0800 | - | 1 | 1 | 0 |
| 0x0D | Unbekannter Alarmtrigger 5 | 0/1 | low | 0x1000 | - | 1 | 1 | 0 |
| 0x0E | Unbekannter Alarmtrigger 6 | 0/1 | low | 0x2000 | - | 1 | 1 | 0 |
| 0x0F | Unbekannter Alarmtrigger 7 | 0/1 | low | 0x4000 | - | 1 | 1 | 0 |
| 0x10 | Unbekannter Alarmtrigger 8 | 0/1 | low | 0x8000 | - | 1 | 1 | 0 |
| 0x11 | Datum | Month | - | unsigned char | - | 1 | 1 | 0 |
| 0x12 | Datum | Day | - | unsigned char | - | 1 | 1 | 0 |
| 0x13 | Datum | Hour | - | unsigned char | - | 1 | 1 | 0 |
| 0x14 | Datum | Minutes | - | unsigned char | - | 1 | 1 | 0 |
| 0x15 | Position Fensterheber Fahrerseite vorne | 0-n | low | 0x0003 | PowerWindowDriver_Status | 1 | 1 | 0 |
| 0x16 | Position Fensterheber Beifahrerseite vorne | 0-n | low | 0x0030 | PowerWindowPassenger_Status | 1 | 1 | 0 |
| 0x17 | Position Schiebedach | 0-n | low | 0x0300 | SHD_Status | 1 | 1 | 0 |
| 0x18 | Neigungspostion Schiebedach | 0-n | low | 0x3000 | SHD_Tilt_Status | 1 | 1 | 0 |
| 0x19 | Aussentemperatur | ºC | - | unsigned char | - | 0.5 | 1 | -40 |
| 0xXY | Unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC801 | ERR_SWITCH_RESET_SVAUS |
| 0xC802 | ERR_SWITCH_RESET_WAKEUP |
| 0xC803 | ERR_SWITCH_RESET_NOT_SLEEP |
| 0xC804 | ERR_SWITCH_OFF_STROMZWEIG |
| 0xC805 | ERR_SWITCH_OFF_WAKEUP |
| 0xC806 | ERR_SWITCH_OFF_NOT_SLEEP |
| 0xC807 | ERR_SWITCH_OFF_TRANSPORT |
| 0xC808 | ERR_POWERDOWN_NOT_SLEEP |
| 0xC809 | ERR_POWERDOWN_WAKEUP |
| 0xC80A | DIAG_CAN_KOMMUNIKATION |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Relativzeit | s | high | signed long | - | 1 | 1 | 0 |
| 0xXY | Unbekannte UW | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-energysaving"></a>
### ENERGYSAVING

Dimensions: 5 rows × 3 columns

| E_MODE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | ENERGY_MODE_AUS | Energiesparmode aus |
| 0x01 | ENERGY_MODE_PRODUCTION | Energiesparmode Produktionsmode |
| 0x02 | ENERGY_MODE_SHIPMENT | Energiesparmode Transportmode |
| 0x04 | ENERGY_MODE_REPAIR_SHOP | Energiesparmode Werkstattmode |
| 0x08 | ERROR | falscher Eingabewert |

<a id="table-eeprom-init-table"></a>
### EEPROM_INIT_TABLE

Dimensions: 4 rows × 3 columns

| ACTION_NUMBER | ACTION_BYTE | ACTION_NAME |
| --- | --- | --- |
| 0x00 | CODING | default Codierung |
| 0x01 | DTC | Fehlerspeicher löschen |
| 0x02 | ALL | EEPROM vollständig löschen |
| 0xXY | -- | -- |

<a id="table-variant-table"></a>
### VARIANT_TABLE

Dimensions: 4 rows × 3 columns

| VARIANT_NUMBER | VARIANT_BYTE | VARIANT_NAME |
| --- | --- | --- |
| 0x00 | LOW | LOW-Variante |
| 0x01 | HIGH | HIGH-Variantw |
| 0x02 | HIGH_MSA | HIGH-Variante mit MSA |
| 0xXY | -- | -- |

<a id="table-dwa-status-tabelle"></a>
### DWA_STATUS_TABELLE

Dimensions: 15 rows × 2 columns

| STAT_DWA_NUMBER | STAT_DWA_NAME |
| --- | --- |
| 0x00 | DWA entschärft |
| 0x01 | DWA schärft |
| 0x02 | DWA geschärft |
| 0x03 | DWA entschärfen |
| 0x04 | DWA Alarm |
| 0x05 | DWA Pause nach Alarm |
| 0x06 | DWA Transportmode |
| 0x07 | DWA Werkstattmode |
| 0x08 | DWA Fertigungsmode |
| 0x09 | DWA geschärft - USIS und Neigungsgeber deaktiviert durch Anwender |
| 0x0D | DWA Panikalarm mode |
| 0x0F | DWA geschärft - USIS und Neigungsgeber nicht aktiv |
| 0x10 | DWA geschärft - USIS nicht aktiv |
| 0x11 | DWA geschärft - Neigungsgeber nicht aktiv |
| 0xXY | -- |

<a id="table-wakeupreason-table"></a>
### WAKEUPREASON_TABLE

Dimensions: 8 rows × 2 columns

| WAKEUP_NUMBER | WAKEUP_REASON_NAME |
| --- | --- |
| 0x00 | NICHT |
| 0x01 | PT_WAKE_UP |
| 0x02 | DWA_NG |
| 0x03 | DWA_INRS |
| 0x04 | TRUNK_CONTACT |
| 0x05 | TRUNK_BUTTON |
| 0x06 | K_CAN_BUS |
| 0xXY | -- |

<a id="table-dwa-historienspeicher-triggers"></a>
### DWA_HISTORIENSPEICHER_TRIGGERS

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F | 0x10 |

<a id="table-dwa-historienspeicher-date"></a>
### DWA_HISTORIENSPEICHER_DATE

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x11 | 0x12 | 0x13 | 0x14 |

<a id="table-dwa-historienspeicher-windows"></a>
### DWA_HISTORIENSPEICHER_WINDOWS

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x15 | 0x16 | 0x17 | 0x18 |

<a id="table-powerwindowdriver-status"></a>
### POWERWINDOWDRIVER_STATUS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Fenster geschlossen |
| 0x0001 | Position mittig |
| 0x0002 | Fesnter offen |
| 0x0003 | ungültiges Signal |
| 0xXY | ungültiges Signal |

<a id="table-powerwindowpassenger-status"></a>
### POWERWINDOWPASSENGER_STATUS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Fenster geschlossen |
| 0x0010 | Position mittig |
| 0x0020 | Fesnter offen |
| 0x0030 | ungültiges Signal |
| 0xXY | ungültiges Signal |

<a id="table-shd-status"></a>
### SHD_STATUS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | SHD nicht offen |
| 0x0100 | Position mittig |
| 0x0200 | SHD offen |
| 0x0300 | ungültiges Signal |
| 0xXY | ungültiges Signal |

<a id="table-shd-tilt-status"></a>
### SHD_TILT_STATUS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | SHD nicht in Position gehoben |
| 0x1000 | Position mittig |
| 0x2000 | SHD in Position gehoben |
| 0x3000 | ungültiges Signal |
| 0xXY | ungültiges Signal |

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

Dimensions: 30 rows × 4 columns

| DINNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | HECKWISCHER_2_RSK | Heckscheibenwischer 2 in Parkposition          	.PIN 27, PORT P1.4 | EIN RSK: 0, AUS RSK: 1 |
| 0x01 | MSA_TASTER | Taster Motor Start/Stop Automatik           .PIN 29, PORT P1.6 | KEINE BETÄTIGUNG: 0, TASTER GEDRÜCKT: 1 |
| 0x02 | SPORT_TASTER | Taster SPORT                           .PIN 30, PORT P1.7 | KEINE BETÄTIGUNG: 0, TASTER GEDRÜCKT: 1 |
| 0x03 | HANDBREMSE_KONTAKT | Schalter Handbremse                       .PIN 32, PORT P1.9 | KEINE BETÄTIGUNG (Handbremse Aus): 0, TASTER GEDRÜCKT (Handbremse Ein): 1 |
| 0x04 | FRONTWISCHER_RSK | Frontscheibenwischer in Parkposition              .PIN 33, PORT P1.10 | EIN RSK: 0, AUS RSK: 1 |
| 0x05 | HECKWISCHER_RSK | Heckscheibenwischer in Parkposition               .PIN 34, PORT P1.11 | EIN RSK: 0, AUS RSK: 1 |
| 0x06 | PTWAKE_IN | PT CAN Wake-Up Input Interrupt line    .PIN 35, PORT P1.12 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x07 | FRONTSCHEIBENHEIZUNG_DIAG | Diagnose Relais Frontscheibenheizung    .PIN 79, PORT P3.10 | OK : 0, FEHLER: 1 |
| 0x08 | KL30G_F2_OFF_DIAG | Diagnose Bistabiles Relais aus MSA     	.PIN 104, PORT P4.10 | AUS: 0, EIN: 1 |
| 0x09 | KL30G_F2_ON_DIAG | Diagnose Bistabiles Relais ein MSA     	.PIN 107, PORT P4.13 | AUS: 0, EIN: 1 |
| 0x0A | HECKWISCHER_2_DIAG | Diagnose Heckscheibenwischer 2     			.PIN 113, PORT P5.3 | AUS: 0, EIN: 1 |
| 0x0B | HECKSCHEIBENHEIZUNG_DIAG | Diagnose Relais Heckscheibenheizung     .PIN 124, PORT P5.14 | AUS: 0, EIN: 1 |
| 0x0C | HECKKLAPPE_TASTER_SEK | Schalter Entriegelung zweite Splitdoor   	.PIN 129, PORT P6.0 | KEINE BETÄTIGUNG: 0, TASTER GEDRÜCKT: 1 |
| 0x0D | HECKKLAPPE_TASTER | Taster Heckklappe öffnen                .PIN 130, PORT P6.1 | KEINE BETÄTIGUNG: 0, TASTER GEDRÜCKT: 1 |
| 0x0E | HECKKLAPPE_KONTAKT | Heckklappenkontakt                       .PIN 131, PORT P6.2 | GESCHLOSSEN: 0, OFFEN: 1 |
| 0x0F | ULTRASCHALLSENSOR | Ultraschallsensor                      .PIN 133, PORT P6.4 | AUS oder NICHT AKTIV: 0 (100 ms.), EIN (1000 ms) oder AKTIV: 1 |
| 0x10 | DSC_TASTER | Taster ASC/DSC                         .PIN 134, PORT P6.5 | KEINE BETÄTIGUNG: 0, TASTER GEDRÜCKT: 1 |
| 0x11 | WASCHWASSERSTAND | Sensor Waschwasser                    .PIN 135, PORT P6.6 | Normaler Füllstand: 0, Zu niedriger Füllstand: 1 |
| 0x12 | KUEHLMITTELSTAND | Sensor Kühlmittelstand                   .PIN 136, PORT P6.7 | Normaler Füllstand: 0, Zu niedriger Füllstand: 1 |
| 0x13 | KIPPSENSOR | Status Neigungsgeber                     .PIN 139, PORT P6.10 | NICHT AKTIV: 0, AKTIV: 1 (500 ms.) |
| 0x14 | KL15_UC_HW_INPUT | KL15 physikalisch                     		.PIN 144, PORT P6.15 | KL15 OFF: 0, KL15 ON: 1 |
| 0x15 | FH_BFTH_ZU_DIAG | Diagnose Fensterheber hinten zu    		.SPI_relays_feedback.OUT0 | AUS: 0, EIN: 1 |
| 0x16 | FH_BFTH_AUF_DIAG | Diagnose Fensterheber hinten auf 		.SPI_relays_feedback.OUT1 | AUS: 0, EIN: 1 |
| 0x17 | FRONTWISCHER_GESCHW_1_DIAG | Diagnose Frontscheibenwischer Geschwindigkeitsrelais 1    .SPI_relays_feedback.OUT2 | AUS: 0, EIN: 1 |
| 0x18 | HECKSCHEIBENHEIZUNG_DIAG | Diagnose Heckscheibenheizung     		.SPI_relays_feedback.OUT3 | AUS: 0, EIN: 1 |
| 0x19 | FRONTWISCHER_GESCHW_2_DIAG | Diagnose Frontscheibenwischer Geschwindigkeitsrelais 2    .SPI_relays_feedback.OUT4 | AUS: 0, EIN: 1 |
| 0x1A | SIRENE_DWA_DIAG | Diagnose Alarmstatus                 .SPI_relays_feedback.OUT5 | AUS: 0, EIN: 1 |
| 0x1B | BISTABILRELAIS_ON_2_DIAG | Diagnose Bistabiles Relais 2 ein          .SPI_relays_feedback.OUT6 | AUS: 0, EIN: 1 |
| 0x1C | GEBLAESEMOTOR_RELAIS_DIAG | Diagnose Relais Motorlüfter          	.SPI_relays_feedback.OUT7 | AUS: 0, EIN: 1 |
| 0xFF | UNKNOWN | unbekannter digitaler Eingang |  |

<a id="table-digitaloutputnrtexte"></a>
### DIGITALOUTPUTNRTEXTE

Dimensions: 37 rows × 4 columns

| DOUTNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | ZV_AUSGANG | Ausgang Zentralverriegelung | Aus: 0, Entriegeln: 1, Selektiv Entriegeln: 3, Verriegeln: 10, Entsichern: 11, Sichern: 14 |
| 0x01 | ZV_ENTRIEGELN_RELAIS | Zentralverriegelung Relais entriegeln           .PIN 1, PORT P0.0 | AUS: 0, EIN: 1 |
| 0x02 | ZV_VERRIEGELN_RELAIS | Zentralverriegelung Relais verriegeln             .PIN 2, PORT P0.1 | AUS: 0, EIN: 1 |
| 0x03 | ZV_ZENTRALSICHERN_RELAIS | Zentralverriegelung Relais sichern           .PIN 3, PORT P0.2 | AUS: 0, EIN: 1 |
| 0x04 | ZV_VERRIEGELN_FAHRERTUERE_RELAIS | Zentralverriegelung Relais verriegeln Fahrer      .PIN 4, PORT P0.3 | AUS: 0, EIN: 1 |
| 0x05 | HECKWISCHER | Heckscheibenwischer                             .PIN 7, PORT P0.4 | AUS: 0, EIN: 1 |
| 0x06 | SRA | Scheinwerferreinigungsanlage                      .PIN 9, PORT P0.6 | AUS: 0, EIN: 1 |
| 0x07 | KLIMAKOMPRESSOR | Klimakompressor                     .PIN 11, PORT P0.8 | AUS: 0, EIN: 1 |
| 0x08 | DUO_WASCHERPUMPE_AUSGANG | Ausgang Waschwasserpumpe | Keine Aktion: 0 oder 3, Vorderes Waschen: 1, Hinteres Waschen: 2 |
| 0x09 | DUO_WASCHERPUMPE_VORNE | Waschwasserpumpe vorne                      .PIN 12, PORT P0.9 | AUS: 0, EIN: 1 |
| 0x0A | DUO_WASCHERPUMPE_HINTEN  | Waschwasserpumpe hinten                      	.PIN 13, PORT P0.10 | AUS: 0, EIN: 1 |
| 0x0B | BISTABILRELAIS_ON | Bistabiles Relais ein                      .PIN 14, PORT P0.11 | AUS: 0, EIN: 1 (5 ms &lt; Tein &lt; 1s), Ausruhen der Zeit zwischen Pulses: 1s |
| 0x0C | BISTABILRELAIS_OFF | Bistabiles Relais aus                     .PIN 18, PORT P0.13 | AUS: 0, EIN: 1 (5 ms &lt; Tein &lt; 1s), Ausruhen der Zeit zwischen Pulses: 1s |
| 0x0D | SCHLAFEN_STRATEGIE | Schlafen-Strategie                         .PIN 19, PORT P0.14 | DISABLE: 0, ENABLE: 1 |
| 0x0E | KL15_EJB | KL15 EJB (Relais)            .PIN 20, PORT P0.15 | AUS: 0, EIN: 1 |
| 0x0F | USIS | Aktivierung Spannungsversorgung USIS    .PIN 23, PORT P1.2 | LOW: 0, HIGH: 1 (12 V im Sensor) |
| 0x10 | GANG_RUCKWAERTS | Status Rückwärtsgang für EC-Spiegel      .PIN 24, PORT P1.3 | AUS: 0, EIN: 1 |
| 0x11 | PORT_AUCSENSOR | Aktivierung AUC-Sensor                      .PIN 42, PORT P2.3 | ENABLE: 0, DISABLE: 1 |
| 0x12 | HECKKLAPPE_MOTOR | Öffnen Heckklappenkontakt                      .PIN 57, PORT P2.10 | AUS: 0, EIN: 1 |
| 0x13 | KL30SW_ENABLE | KL30 SW-Aktivierung                         .PIN 59, PORT P2.12 | DISABLE: 0, ENABLE: 1 |
| 0x14 | PTWAKE_OUT | PT CAN Wake-Up Output Interrupt line   .PIN 62, PORT P2.15 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x15 | FRONTSCHEIBENHEIZUNG | Relais Frontscheibenheizung              .PIN 100, PORT P4.6 | AUS: 0, EIN: 1 |
| 0x16 | ULTRASCHALL_SIRENE_ENABLE | Aktivierung interene Überwachung / Sirene.PIN 101, PORT P4.7 | DISABLE: 0, ENABLE: 1 |
| 0x17 | KL30G_F2_OFF | Bistabiles Relais aus MSA                .PIN 103, PORT P4.9 | AUS: 0, EIN: 1 (5 ms &lt; Tein &lt; 1s), Ausruhen der Zeit zwischen Pulses: 1s |
| 0x18 | KL30G_F2_ON | Bistabiles Relais ein MSA                 .PIN 104, PORT P4.11 | AUS: 0, EIN: 1 (5 ms &lt; Tein &lt; 1s), Ausruhen der Zeit zwischen Pulses: 1s |
| 0x19 | HECKWISCHER_2 | Heckscheibenwischer 2                           .PIN 114, PORT P5.4 | AUS: 0, EIN: 1 |
| 0x1A | HECKKLAPPE_2_MOTOR | Öffnen Heckklappe 2                    .PIN 118, PORT P5.8 | AUS: 0, EIN: 1 |
| 0x1B | BISTABILRELAIS_OFF_2 | Bistabiles Relais aus 2                   .PIN 123, PORT P5.13 | AUS: 0, EIN: 1 (5 ms &lt; Tein &lt; 1s), Ausruhen der Zeit zwischen Pulses: 1s |
| 0x1C | FH_BFTH_ZU | Fensterheber hinten zu              		.SPI_relays_out.OUT0 | AUS: 0, EIN: 1 |
| 0x1D | FH_BFTH_AUF | Fensterheber hinten auf           		.SPI_relays_out.OUT1 | AUS: 0, EIN: 1 |
| 0x1E | FRONTWISCHER_GESCHW_1 | Frontscheibenwischer Geschwindigkeitsrelais 1              .SPI_relays_out.OUT2 | AUS: 0, EIN: 1 |
| 0x1F | HECKSCHEIBENHEIZUNG | Heckscheibenheizung                     .SPI_relays_out.OUT3 | AUS: 0, EIN: 1 |
| 0x20 | FRONTWISCHER_GESCHW_2 | Frontscheibenwischer Geschwindigkeitsrelais 2              .SPI_relays_out.OUT4 | AUS: 0, EIN: 1 |
| 0x21 | SIRENE_DWA | Aktivierung Sirene                       .SPI_relays_out.OUT5 | AUS: 0, EIN: 1 |
| 0x22 | BISTABILRELAIS_ON_2 | Bistabiles Relais ein 2                    .SPI_relays_out.OUT6 | AUS: 0, EIN: 1 (5 ms &lt; Tein &lt; 1s), Ausruhen der Zeit zwischen Pulses: 1s |
| 0x23 | GEBLAESEMOTOR_RELAIS | Relais Motorlüfter                    	.SPI_relays_out.OUT7 | AUS: 0, EIN: 1 |
| 0xFF | UNKNOWN | unbekannter digitaler Ausgang |  |

<a id="table-analoginputnrtexte"></a>
### ANALOGINPUTNRTEXTE

Dimensions: 14 rows × 4 columns

| AINNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | HECKKLAPPE_2_MOTOR_DIAG | Diagnose Öffnen Heckklappe 2          .PIN 72, PORT P3.5 | OPEN-LOAD: 0....60(0x3C), OK: 61(0x3D).....920(0x398), SHORT-GND: 921(0x399)....1023(0x3FF) |
| 0x01 | BATTERIE_SPANNUNG | Spannungsversorgung                        .PIN 73, PORT P3.6 | 0(0 V)...0x3FF(1023)(18.50 V) (HEX);(HEX)=Vbat*5530/100  [V] |
| 0x02 | FH_HINTEN_SCHALTER | Taster Fensterheber hinten               .PIN 74, PORT P3.7 | DOWNAUTO(2):0x08F..0x15A,DOWNMANUAL(1):0x15B..0x23B,UPAUTO(4):0x23C..0x2F4,UPMANUAL(3):0x2F5..0x3B7,OFF(0):0x3B8..0x3FF |
| 0x03 | TANK_FA_FUELLSTAND | Tankgeber links            .PIN 77, PORT P3.8 | 0...0x3FF(1023); (HEX)=(8388,6*Vbat*RS)/(18,12+151*RS); Full:20 Ohm, Empty: 475 Ohm (40 ltr.) or 295 Ohm (50 ltr.), SHORT-GND: &lt; 10 Ohm, OPEN-LOAD: &gt; 550 Ohm (40 ltr.) or 350 Ohm (50 ltr.) |
| 0x04 | TANK_BF_FUELLSTAND | Tankgeber rechts           .PIN 78, PORT P3.9 | 0...0x3FF(1023); (HEX)=(8388,6*Vbat*RS)/(18,12+151*RS); Full:20 Ohm, Empty: 475 Ohm (40 ltr.) or 295 Ohm (50 ltr.), SHORT-GND: &lt; 10 Ohm, OPEN-LOAD: &gt; 550 Ohm (40 ltr.) or 350 Ohm (50 ltr.) |
| 0x05 | HECKBREMSBELAGVERSCHLEISS | Verschleiss Bremsbelag hinten                         .PIN 80, PORT P3.11 | STAGE 0(&lt;5 Ohm): 0...203(0xCB), STAGE 1(470 Ohm ± 10%): 204(0xCC)...982(0x3D6) (Vbatt&gt;=10.5V) or 204(0xCC)...818(0x332) (Vbatt&lt;10.5V), STAGE 12(&gt; 100 kOhm): &gt;982(0x3D6) (Vbatt&gt;=10.5V) or &gt;818(0x332) (Vbatt&lt;10.5V) |
| 0x06 | FRONTBREMSBELAGVERSCHLEISS | Verschleiss Bremsbelag vorne                        .PIN 81, PORT P3.12 | STAGE 0(&lt;5 Ohm): 0...203(0xCB), STAGE 1(470 Ohm ± 10%): 204(0xCC)...982(0x3D6) (Vbatt&gt;=10.5V) or 204(0xCC)...818(0x332) (Vbatt&lt;10.5V), STAGE 12(&gt; 100 kOhm): &gt;982(0x3D6) (Vbatt&gt;=10.5V) or &gt;818(0x332) (Vbatt&lt;10.5V) |
| 0x07 | HECKKLAPPE_MOTOR_DIAG | Diagnose Öffnen Heckklappe            .PIN 82, PORT P3.13 | OPEN-LOAD: 0....60(0x3C), OK: 61(0x3D).....920(0x398), SHORT-GND: 921(0x399)....1023(0x3FF) |
| 0x08 | WASCHDUESENHEIZUNG_AUSSENSPIEGEL_DIAG | Diagnose Spritzdüsen- und Aussenspiegelheizung  .PIN 84, PORT P3.15 | OPEN-LOAD: 0....60(0x3C), OK: 61(0x3D).....920(0x398), SHORT-GND: 921(0x399)....1023(0x3FF) |
| 0x09 | AUCSENSOR | AUC Sensor PWM                         .PIN 17, PORT P0.12 | AUCSENSOR_PERIOD: 0..131 ms, AUCSENSOR_DUTY_CYCLE: 0..100 %; NORMAL: Period=20 ms (50 Hz) Duty-cycle=5%-95%, SHORT-GND: Period=0 Duty-cycle=0, OPEN-LOAD: Duty-cycle=0xFFFF |
| 0x0A | SITZHEIZUNG_FA_DIAG | Diagnose Sitzheizung Fahrer          .PIN 21, PORT P1.0 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x0B | SITZHEIZUNG_BF_DIAG | Diagnose Sitzheizung Beifahrer       .PIN 22, PORT P1.1 | NICHT AKTIV: 0, AKTIV: 1 |
| 0x0C | DCDC_MSA | Diagnose MSA DC/DC Converter PWM      .PIN 94, PORT P4.0 | DCDC_MSA_PERIOD: 0..131 ms, DCDC_MSA_DUTY_CYCLE: 0..100 %; NORMAL: Period=0 Duty-cycle=0, OPEN-LOAD: Duty-cycle=0xFFFF, OVERTEMPERATURE: Period= 77 ms(13 Hz) Duty-cycle=20%-80% |
| 0xFF | UNKNOWN | unbekannter analoger Ausgang |  |

<a id="table-analogoutputnrtexte"></a>
### ANALOGOUTPUTNRTEXTE

Dimensions: 8 rows × 4 columns

| AOUTNR | NAME | TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | SPORT_LED_PWM | Sport LED                              		.PIN 31, PORT P1.8 | 0...100 % |
| 0x01 | LED_HEARTBEAT_PWM | DWA-LED Tastverhältnis PWM-Signal für Heartbeat-Simulation .PIN 43,PORT P2.4 | 0...100 % |
| 0x02 | LED_DWA_PWM | DWA-LED Tastverhältnis PWM-Signal                .PIN 44, PORT P2.5 | OFF: 0, FLASHING: 1 (F=0.5 Hz. 50 ms ON), BLINKING: 2 (F=2 Hz. 250 ms ON), ON: 3 |
| 0x03 | SITZHEIZUNG_FA_PWM | Sitzheizung Fahrer Tastverhältnis PWM-Signal      .PIN 45, PORT P2.6 | OFF: 0 (40ms ON), STATE1: 1 (32ms ON, 8ms OFF), STATE2: 2 (20ms ON, 20ms OFF), STATE3: 3 (12ms ON, 28ms OFF) |
| 0x04 | SITZHEIZUNG_BF_PWM | Sitzheizung Beifahrer Tastverhältnis PWM-Signal   .PIN 46, PORT P2.7 | OFF: 0 (40ms ON), STATE1: 1 (32ms ON, 8ms OFF), STATE2: 2 (20ms ON, 20ms OFF), STATE3: 3 (12ms ON, 28ms OFF) |
| 0x05 | WASCHDUESENHEIZUNG_AUSSENSPIEGEL | Spritzdüsen- und Aussenspiegelheizung     .PIN 58, PORT P2.11 | AUS: 0, EIN: 1 |
| 0x06 | MSA_LED_PWM | MSA LED                                		.PIN 112, PORT P5.2 | 0...100 % |
| 0xFF | UNKNOWN | unbekannter analoger Ausgang |  |
