# KGM_60.prg

- Jobs: [123](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KGM_60 |
| ORIGIN | BMW EI-61 Herter |
| REVISION | 3.005 |
| AUTHOR | LEAR DCS Ahrens, LEAR DCS Scheler, LEAR DCS Schmidt |
| COMMENT | N/A |
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
- [_CODIERDATEN_BLOCK_LESEN_LEAR](#job-codierdaten-block-lesen-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [_CODIERDATEN_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten Modus  : Codieren je nach Block
- [_CODIERDATEN_3900_LESEN_KOMPLETT_LEAR](#job-codierdaten-3900-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3900-Bereich Auslesen der KGM-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3900_SCHREIBEN_AUS_DATEI_LEAR](#job-codierdaten-3900-schreiben-aus-datei-lear) - Beschreiben der Default-Codierdaten Beschreiben der KGM-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $39xx Codierdaten, Default Modus  : Default
- [_CODIERDATEN_3800_LESEN_KOMPLETT_LEAR](#job-codierdaten-3800-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3800-Bereich Auslesen der KGM-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3800_SCHREIBEN_AUS_DATEI_LEAR](#job-codierdaten-3800-schreiben-aus-datei-lear) - Beschreiben der Default-Codierdaten Beschreiben der KGM-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $38xx Codierdaten, Default Modus  : Default
- [_FEHLERSPEICHER_EEPROM_LOESCHEN_LEAR](#job-fehlerspeicher-eeprom-loeschen-lear) - KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [STATUS_MICROPOWERMODULE](#job-status-micropowermodule) - Auslesen der Zustände und Funktions-Variablen vom Modul MPM Das MPM-Relais schaltet die Klemme 30g_f KWP2000: $30 InputOutputControlByLocalIdentifier $20 MPM_VAR_READ $01 ReportCurrentState
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Inputs $01 ReportCurrentState
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $02 Analoge Inputs $01 ReportCurrentState
- [STATUS_LICHT](#job-status-licht) - Auslesen der Zustände und Variablen vom Modul ASL/VFB (Ausstiegsleuchte/Vorfeldbeleuchtung) KWP2000: $30 InputOutputControlByLocalIdentifier $21 ESL_VAR_READ $01 ReportCurrentState
- [STATUS_SCHALTERBLOCK_TUER](#job-status-schalterblock-tuer) - Auslesen der Variablen vom Modul LSB (LIN-Schalterblock) KWP2000: $30 InputOutputControlByLocalIdentifier $22 LSB_VAR_READ $01 ReportCurrentState
- [STATUS_SERVOTRONIC](#job-status-servotronic) - Auslesen der Zustände und Variablen vom Funktions-Modul SVT (Servotronic) KWP2000: $30 InputOutputControlByLocalIdentifier $23 SVT_VAR_READ $01 ReportCurrentState
- [STATUS_MEMORY_POSITION_SPIEGEL](#job-status-memory-position-spiegel) - Abfrage der MemoryPosition der beiden Aussenspiegel KWP2000: $30 InputOutputControlByLocalIdentifier $0A Position Spiegel $01 ReportCurrentState
- [_STATUS_READ_VARS_COMICRO](#job-status-read-vars-comicro) - Auslesen der Variablen vom Funktions-Modul Co-Microprozessor KWP2000: $30 InputOutputControlByLocalIdentifier $26 COMICRO_VAR_READ $01 ReportCurrentState
- [STATUS_ZENTRALVERRIEGELUNG](#job-status-zentralverriegelung) - Auslesen der Variablen vom Funktions-Modul Zentralverriegelung KWP2000: $30 InputOutputControlByLocalIdentifier $27 ZV__VAR_READ $01 ReportCurrentState
- [STATUS_SCHLOSSNUESSE](#job-status-schlossnuesse) - Auslesen der Variablen vom Funktions-Modul Schaltnuss KWP2000: $30 InputOutputControlByLocalIdentifier $28 SNU_VAR_READ $01 ReportCurrentState
- [STATUS_BUSLAST](#job-status-buslast) - Daten zur Buslast KWP2000: $30 InputOutputControlByLocalIdentifier $2A ESL_VAR_READ $01 ReportCurrentState
- [_STATUS_BIOS_VIRT_SIG](#job-status-bios-virt-sig) - Auslesen der Bussignale KWP2000: $30 InputOutputControlByLocalIdentifier $2B BIOS_VAR_READ $01 ReportCurrentState
- [STATUS_SPIEGEL](#job-status-spiegel) - Auslesen der Zustände und Variablen vom Modul LIN-Spiegel (Außenspiegel FA/BF) KWP2000: $30 InputOutputControlByLocalIdentifier $24 ASP_VAR_READ $01 ReportCurrentState
- [STEUERN_MICROPOWERMODULE](#job-steuern-micropowermodule) - Vorgabe der Relaiszustaende des MicroPowerModuls KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $03 MPM Outputs
- [STEUERN_LICHT](#job-steuern-licht) - Vorgabe der Schaltzustaende der Ausstiegsleuchte ASL, Vorfeldbeleuchtung VFB Und LED´s des Schalterblocks KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $04 ESL Outputs
- [STEUERN_POSITION_SPIEGEL](#job-steuern-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel
- [STEUERN_SPIEGEL_ABBLENDEN](#job-steuern-spiegel-abblenden) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel Abblenden der Aussenspiegel
- [STEUERN_SPIEGELHEIZUNG](#job-steuern-spiegelheizung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel Spiegelheizung mit speziellen Werten eischalten
- [STEUERN_MEMORY_POSITION_SPIEGEL](#job-steuern-memory-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel Memory Schreiben der MemoryPosition der beiden Aussenspiegel
- [STEUERN_POSITION_DIREKT_SPIEGEL](#job-steuern-position-direkt-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel ausgewaehlten Spiegel in angegebene Position fahren
- [STEUERN_SERVOTRONIC](#job-steuern-servotronic) - Steuerung des Stromwandlers KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $05 SVT Outputs
- [STEUERN_ZENTRALVERRIEGELUNG](#job-steuern-zentralverriegelung) - Vorgabe der Schaltzustaende der Zentralverriegelung KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $08 ZV__OUTPUTS
- [STEUERN_SITZHEIZUNG](#job-steuern-sitzheizung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0D Steuern Sitzheizung
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_1](#job-status-historienspeicher-lesen-block-1) - EnergieDatenSpeicher Teil 1 -Einschlafverhinderer- auslesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE0 commonProjectSpecific
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_2](#job-status-historienspeicher-lesen-block-2) - EnergieDatenSpeicher Teil 2 -Wecker- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE1 commonProjectSpecific
- [STATUS_HISTORIENSPEICHER_LESEN_BLOCK_3](#job-status-historienspeicher-lesen-block-3) - EnergieDatenSpeicher Teil 3 - Wecker-ID - auslesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific
- [STEUERN_HISTORIENSPEICHER_LOESCHEN](#job-steuern-historienspeicher-loeschen) - EnergieDatenSpeicher loeschen KWP 2000: $22   WriteDataByCommonIdentifier KWP 2000: $EFE3 commonProjectSpecific
- [_FLASH_COMICRO](#job-flash-comicro) - Internen Flashvorgang des Co-Prozessors anstossen KWP 2000: $2E   WriteDataByCommonIdentifier KWP 2000: $EFE4 commonProjectSpecific
- [_BRIF_SCHREIBEN_LEAR](#job-brif-schreiben-lear) - Beschreiben der BRIF-Inhalte KWP 2000: $3B ApplDiagWriteDataByLocalIdentifier Modus   : 0x70 Modus  : Default
- [_LEAR_PROD_DATEN_SCHREIBEN](#job-lear-prod-daten-schreiben) - Beschreiben von Teilen des BRIF, laufenden SG-Nur., Produktionsdatum Es muessen immer alle Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $3B WriteDataByCommonIdentifier $70 BRIF schreiben Modus  : Default
- [_HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $72 Herstellerdaten Modus  : Default
- [_HERSTELLERDATEN_SCHREIBEN](#job-herstellerdaten-schreiben) - Beschreiben der Herstellerdaten Es muessen immer alle Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $3B WriteDataByCommonIdentifier $71 Herstellerdaten Modus  : Default
- [_LINKINFO_GWVERSION_LESEN](#job-linkinfo-gwversion-lesen) - Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $73 LinkInfo Modus  : Default
- [_KGM_SEND_MESSAGE](#job-kgm-send-message) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $31 StartRoutineByLocalIdentifier $11 CommonSwitch
- [STATUS_FENSTERHEBER](#job-status-fensterheber) - Stati der einzelnen FH-Funktionen auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReportCurrentState
- [_STATUS_FH_ADAPTIONSWERTE](#job-status-fh-adaptionswerte) - Die Adaptionswerte sind ein Maß der mechanischen Güte des FH-Antriebs Auswertung grafisch linear (f-&gt;f(x), x = Byteposition, f = Bytewert) Modus  : Default KWP2000: $22 ReadDataByCommonIdentifier $37xx Speicherdaten je nach FH-Seite
- [STATUS_FH_DENORM_LOGGER_LOESCHEN](#job-status-fh-denorm-logger-loeschen) - Denormierungslogger löschen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $07 ShortTimeAccess
- [STATUS_FH_LOGGER_DENORMIERER](#job-status-fh-logger-denormierer) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen der letzten drei Einträge von EE_FH_LOG_DATA
- [_STATUS_FH_DENORMIERUNGS_LOGGER_LESEN](#job-status-fh-denormierungs-logger-lesen) - Fensterheber Denorierungslogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReadCurrentState $14 SUBSWITCH
- [STATUS_FH_LOGGER_REVERSIERER](#job-status-fh-logger-reversierer) - Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReadCurrentState $16 SUBSWITCH
- [_STATUS_FH_REVERSIERUNGS_LOGGER_LESEN](#job-status-fh-reversierungs-logger-lesen) - Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReadCurrentState $16 SUBSWITCH
- [_STEUERN_FENSTERHEBER_DIAGNOSE_BROSE](#job-steuern-fensterheber-diagnose-brose) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 Diagnose Jobs 1-5 fuer BROSE-FH $07 ShortTermAdjustment Status von KGM schreiben
- [STEUERN_FENSTERHEBER_MIT_EKS_EINLERNEN](#job-steuern-fensterheber-mit-eks-einlernen) - Einlernen der Fensterheber mit Einklemmschutz (EKS) KWP2000: $30 InputOutputControlByLocalIdentifier $07 Ansteuern FH $07 ShortTermAdjustment Dauer max. 14sec
- [STEUERN_FENSTERHEBER_DENORMIEREN](#job-steuern-fensterheber-denormieren) - Denormieren der Fensterheber, je nach Auswahl Fahrer, Beifahrer, beide KWP2000: $30 InputOutputControlByLocalIdentifier $07 Ansteuern FH $07 ShortTermAdjustment
- [STEUERN_FENSTERHEBER](#job-steuern-fensterheber) - Ansteuerung des Fensterhebers an der Fahrertuer (FA) und/oder der Beifahrertuer (BF) KWP2000: $30 InputOutputControlByLocalIdentifier $07 Steuern Fensterheber $07 ShortTermAdjustment
- [_STEUERN_FENSTERHEBER_OHNE_EKS](#job-steuern-fensterheber-ohne-eks) - Ansteuerung des Fensterhebers an beiden Tueren ACHTUNG: Einklemmschutz ABGESCHALTET, keine Normierung erforderlich KWP2000: $30 InputOutputControlByLocalIdentifier $07 Steuern Fensterheber $07 ShortTermAdjustment
- [_FH_FAT_KURZHUB_INIT_LEAR](#job-fh-fat-kurzhub-init-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [_FH_BFT_KURZHUB_INIT_LEAR](#job-fh-bft-kurzhub-init-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [_STEUERN_FH_INIT_DICHTUNG_LEAR](#job-steuern-fh-init-dichtung-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [_STATUS_FH_INIT_DICHTUNG_LEAR](#job-status-fh-init-dichtung-lear) - KWP2000: $22 ReadDataByCommonIdentifier $3930 Codierdaten aus Info-Block Modus  : Default
- [STATUS_LADERAUMABDECKUNG](#job-status-laderaumabdeckung) - Status der Laderaumabdeckung (Lara CRoFt) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2C LARA_VAR_READ
- [STEUERN_LADERAUMABDECKUNG](#job-steuern-laderaumabdeckung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0C Steuern Laderaumabdeckung
- [_STEUERN_LARA_LEAR](#job-steuern-lara-lear) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0C Steuern Laderaumabdeckung
- [_LARA_COUNTER_RESET](#job-lara-counter-reset) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default KWP2000: $2E WriteDataByCommonIdentifier Kodierblock lesen, verändern, zurückschreiben
- [_CODIEREN_LCPA](#job-codieren-lcpa) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0e CODIEREN LCPA
- [_CKS_LCPA](#job-cks-lcpa) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0e CKS LCPA
- [READ_LCPA_IDENT](#job-read-lcpa-ident) - ident lesen des LIN-Slave CPA Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-LCPA Modus  : Default Auslesen der Identdaten der LCPA
- [C_FG_SCHREIBEN_LCPA](#job-c-fg-schreiben-lcpa) - Schreiben der FG-Nr. in den LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_FG_LESEN_LCPA](#job-c-fg-lesen-lcpa) - Lesen der FG-Nr. aus dem LCPA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier
- [C_FG_AUFTRAG_LCPA](#job-c-fg-auftrag-lcpa) - Schreiben und Lesen der FG-Nr. LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_AEI_SCHREIBEN_LCPA](#job-c-aei-schreiben-lcpa) - Schreiben des Aenderungsindex in den LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_AEI_LESEN_LCPA](#job-c-aei-lesen-lcpa) - Lesen des Aenderungsindex aus dem LCPA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier
- [C_AEI_AUFTRAG_LCPA](#job-c-aei-auftrag-lcpa) - Schreiben und Lesen des Aenderungsindex LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [RESET_LCPA](#job-reset-lcpa) - Reset LCPA KWP2000: $A6 LINGateway $11 Reset

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

<a id="job-codierdaten-block-lesen-lear"></a>
### _CODIERDATEN_BLOCK_LESEN_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Bereich: 0x30xx bis 0x3Dxx |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | binary | Codierdaten fuer angegebenen Block |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-block-schreiben-lear"></a>
### _CODIERDATEN_BLOCK_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten Modus  : Codieren je nach Block

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | Block+Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3900-lesen-komplett-lear"></a>
### _CODIERDATEN_3900_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3900-Bereich Auslesen der KGM-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_KGM_1 | string | die kompletten Codierdaten im 3900-Bereich (KGM) |
| CODIERDATEN_KGM_2 | string | die kompletten Codierdaten im 3900-Bereich (KGM) |
| CODIERDATEN_KGM_3 | string | die kompletten Codierdaten im 3900-Bereich (KGM) |
| CODIERDATEN_KGM_4 | string | die kompletten Codierdaten im 3900-Bereich (KGM) |
| CODIERDATEN_KGM_5 | string | die kompletten Codierdaten im 3900-Bereich (KGM) |
| CODIERDATEN_KGM_6 | string | die kompletten Codierdaten im 3900-Bereich (KGM) |
| CODIERDATEN_KGM_7 | string | die kompletten Codierdaten im 3900-Bereich (KGM) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3900-schreiben-aus-datei-lear"></a>
### _CODIERDATEN_3900_SCHREIBEN_AUS_DATEI_LEAR

Beschreiben der Default-Codierdaten Beschreiben der KGM-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $39xx Codierdaten, Default Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten fuer 3900-Bereich Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3800-lesen-komplett-lear"></a>
### _CODIERDATEN_3800_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3800-Bereich Auslesen der KGM-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_KGM_1 | string | die kompletten Codierdaten im 3800-Bereich (KGM) |
| CODIERDATEN_KGM_2 | string | die kompletten Codierdaten im 3800-Bereich (KGM) |
| CODIERDATEN_KGM_3 | string | die kompletten Codierdaten im 3800-Bereich (KGM) |
| CODIERDATEN_KGM_4 | string | die kompletten Codierdaten im 3800-Bereich (KGM) |
| CODIERDATEN_KGM_5 | string | die kompletten Codierdaten im 3800-Bereich (KGM) |
| CODIERDATEN_KGM_6 | string | die kompletten Codierdaten im 3800-Bereich (KGM) |
| CODIERDATEN_KGM_7 | string | die kompletten Codierdaten im 3800-Bereich (KGM) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3800-schreiben-aus-datei-lear"></a>
### _CODIERDATEN_3800_SCHREIBEN_AUS_DATEI_LEAR

Beschreiben der Default-Codierdaten Beschreiben der KGM-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $38xx Codierdaten, Default Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten fuer 3800-Bereich Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fehlerspeicher-eeprom-loeschen-lear"></a>
### _FEHLERSPEICHER_EEPROM_LOESCHEN_LEAR

KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-micropowermodule"></a>
### STATUS_MICROPOWERMODULE

Auslesen der Zustände und Funktions-Variablen vom Modul MPM Das MPM-Relais schaltet die Klemme 30g_f KWP2000: $30 InputOutputControlByLocalIdentifier $20 MPM_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MPM_RELAIS | int | momentaner Modul-Status "1", MPM-Relais eingeschalten "0", MPM-Relais ausgeschalten |
| STAT_SV_AUS_TIMER | unsigned long | Zeit in 10 Sekunden-Schritten bis Standverbraucher ausgeschalten werden |
| STAT_KLR_TIMER | unsigned long | Zeit in 10 Sekunden-Schritten nach Klemme R aus |
| STAT_WECKER | int | aktuelle Anzahl der Wecker |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 Digitale Inputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SERVO_ST_EIN | int | Statuspin Treiber von Servopumpe nur fuer Entwicklung |
| STAT_VFB_ST_EIN | int | Statuspin Treiber der Vorfeldbeleuchtung |
| STAT_ESL_ST_EIN | int | Statuspin Treiber der Enstiegsleuchte |
| STAT_SB_VERS_ST_EIN | int | Statuspin Treiber der LIN-Schalterblockversorgung |
| STAT_FH_ZU_IN_EIN | int | Beifahrertuerschalter Eingang 1 |
| STAT_FH_AUF_IN_EIN | int | Beifahrertuerschalter Eingang 2 |
| STAT_HALL_TK_BF_IN_EIN | int | Tuerkontakt Beifahrertuer 0: Tuer zu, 1: Tuer auf |
| STAT_HALL_SZ_VERR_IN_EIN | int | Eingang Schlossnuss 1 |
| STAT_HALL_SZ_ENTR_IN_EIN | int | Eingang Schlossnuss 2 |
| STAT_HALL_TK_FA_IN_EIN | int | Tuerkontakt Fahrertuer 0: Tuer zu, 1: Tuer auf |
| STAT_WUPDAT_EIN | int | Reserve interner Status ohne direkte Aussgae |
| STAT_ST_SERVO_LOW_EIN | int | Status Servopumpe Lowside interner Status ohne direkte Aussgae |
| STAT_FH_FA_HS_1_EIN | int | Hallsensor Fensterheber Fahrerseite 1 |
| STAT_FH_FA_HS_2_EIN | int | Hallsensor Fensterheber Fahrerseite 2 |
| STAT_FH_BF_HS_1_EIN | int | Hallsensor Fensterheber Beifahrerseite 1 |
| STAT_FH_BF_HS_2_EIN | int | Hallsensor Fensterheber Beifahrerseite 2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-inputs"></a>
### STATUS_ANALOG_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $02 Analoge Inputs $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_SERVO_IN_WERT | real | Spannung Servopumpe Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_KL30B_WERT | real | Spannung Klemme 30B Bereich: 0 V bis 18 V von aussen an PIN B33.1 - B33.3 |
| STAT_SPANNUNG_DIAG_FH_BF_WERT | real | Spannung Fensterhebermotor Beifahrer Bereich: 0 V bis 18 V intern |
| STAT_SPANNUNG_KL30_WERT | real | Spannung Klemme 30 Bereich: 0 V bis 18 V von aussen an PIN B38.1 - B38.2 |
| STAT_SPANNUNG_MVRFT_DIAG_WERT | real | Spannung Motor fuer Verriegeln Fahrertuer Bereich: 0 V bis 18 V intern |
| STAT_SPANNUNG_MZS_DIAG_WERT | real | Spannung Motor fuer Sichern beide Tueren Bereich: 0 V bis 18 V intern |
| STAT_SPANNUNG_MER_DIAG_WERT | real | Spannung Motor fuer Entriegeln beide Tueren Bereich: 0 V bis 18 V intern |
| STAT_SPANNUNG_MVR_DIAG_WERT | real | Spannung Motor fuer Verriegeln Beifahrertuer Bereich: 0 V bis 18 V intern |
| STAT_SPANNUNG_ASP_SEN_BF_WERT | real | Spannung Aussenspiegel Sensor Beifahrer Bereich: 0 V bis 5 V intern |
| STAT_SPANNUNG_ASP_SEN_FA_WERT | real | Spannung Aussenspiegel Sensor Fahrer Bereich: 0 V bis 5 V intern |
| STAT_SPANNUNG_KL30A_WERT | real | Spannung Klemme 30A Bereich: 0 V bis 18 V von aussen an PIN A33.1 - A33.3 |
| STAT_SPANNUNG_RESERVE_WERT | real | Reserve, nochnicht belegt Bereich: 0 V bis 5 V intern |
| STAT_SPANNUNG_DIAG_FH_FA_WERT | real | Spannung Fensterhebermotor Fahrer Bereich: 0 V bis 18 V intern |
| STAT_SPANNUNG_EC_IN_WERT | real | Spannung Elektrochrom Bereich: 0 V bis 5 V intern |
| STAT_SPANNUNG_DIAG_MPM_WERT | real | Spannung Mikropowermodul Bereich: 0 V bis 18 V intern |
| STAT_SPANNUNG_HALL_FH_SERV_WERT | real | Spannung Hallsensoren Fensterheber Bereich: 0 V bis 16 V intern |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-licht"></a>
### STATUS_LICHT

Auslesen der Zustände und Variablen vom Modul ASL/VFB (Ausstiegsleuchte/Vorfeldbeleuchtung) KWP2000: $30 InputOutputControlByLocalIdentifier $21 ESL_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ESL | int | "1" wenn Einstiegsleuchte an ist |
| STAT_VFB | int | "1" wenn Vorfeldleuchte an ist |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schalterblock-tuer"></a>
### STATUS_SCHALTERBLOCK_TUER

Auslesen der Variablen vom Modul LSB (LIN-Schalterblock) KWP2000: $30 InputOutputControlByLocalIdentifier $22 LSB_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ASP_WIPPE_TEXT | string | Positionen LINKS, RECHTS, OBEN, UNTEN, NULL |
| STAT_SPIEGEL_TASTER_LINKS_EIN | unsigned int | Fahrerseite (Tastenblock): 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach links zu bewegen |
| STAT_SPIEGEL_TASTER_RECHTS_EIN | unsigned int | Fahrerseite (Tastenblock): 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach rechts zu bewegen |
| STAT_SPIEGEL_TASTER_OBEN_EIN | unsigned int | Fahrerseite (Tastenblock): 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach oben zu bewegen |
| STAT_SPIEGEL_TASTER_UNTEN_EIN | unsigned int | Fahrerseite (Tastenblock): 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach unten zu bewegen |
| STAT_SPIEGEL_TASTER_GESAMT | unsigned int | Fahrerseite (Tastenblock): 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach links zu bewegen 2: Taster gedrueckt, um Spiegel nach oben zu bewegen 3: Taster gedrueckt, um Spiegel nach rechts zu bewegen 4: Taster gedrueckt, um Spiegel nach unten zu bewegen |
| STAT_ASP_RL | string | Positionen LINKS oder RECHTS |
| STAT_SPIEGEL_SCHALTER_FA_EIN | unsigned int | Fahrerseite (Tastenblock): Spiegelauswahl Fahrer, Beifahrer 0: Beifahrerspiegel 1: Fahrerspiegel |
| STAT_ASP_KLAPPEN | int | "1" wenn Beiklapptaste gedrückt |
| STAT_FH_TASTERFA_FA_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Fahrerseite ZU (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FA_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Fahrerseite AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FA_MAUT_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Fahrerseite MAUT ZU (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FA_MAUT_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Fahrerseite MAUT AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FA_GESAMT | unsigned int | Fahrerseite (Tastenblock): Fensterheber Fahrerseite gesamt 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTERFA_BF_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite ZU (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BF_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BF_MAUT_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite MAUT ZU (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BF_MAUT_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite MAUT AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BF_GESAMT | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite gesamt 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTERFA_FAH_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite ZU (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FAH_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FAH_MAUT_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite MAUT ZU (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FAH_MAUT_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite MAUT AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FAH_GESAMT | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite gesamt 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTERFA_BFH_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite ZU (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BFH_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BFH_MAUT_ZU | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite MAUT ZU (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BFH_MAUT_AUF | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite MAUT AUF (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BFH_GESAMT | unsigned int | Fahrerseite (Tastenblock): Fensterheber Beifahrerseite gesamt 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_VO_LI | string | Positionen AUF, ZU, TAUF, TZU, NULL |
| STAT_FH_VO_RE | string | Positionen AUF, ZU, TAUF, TZU, NULL |
| STAT_FH_HI_LI | string | Positionen AUF, ZU, TAUF, TZU, NULL |
| STAT_FH_HI_RE | string | Positionen AUF, ZU, TAUF, TZU, NULL |
| STAT_FNBUT1 | int | "1" wenn Funktionsknopf-1 gedrückt ist |
| STAT_FNBUT2 | int | "1" wenn Funktionsknopf-2 gedrückt ist |
| STAT_FH_FREIGABE | int | "1" wenn FH-Freigabe vom CAS aktiv ist |
| STAT_LED1 | int | "1" wenn Funktionsleuchte 1 an ist |
| STAT_LED2 | int | "1" wenn Funktionsleuchte 2 an ist |
| STAT_SZT_DIMMUNG_WERT | int | Rücklesewert der Dimmung am Schalterblock |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-servotronic"></a>
### STATUS_SERVOTRONIC

Auslesen der Zustände und Variablen vom Funktions-Modul SVT (Servotronic) KWP2000: $30 InputOutputControlByLocalIdentifier $23 SVT_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERBAUT | int | "1" wenn Servotronic verbaut |
| STAT_VERBAUT_TEXT | string | "verbaut" oder "nicht verbaut" |
| STAT_CHKS_ERR | int | "0" wenn kein Checksum Fehler vorhanden "1" wenn Checksum Fehler vorhanden |
| STAT_CHKS_ERR_TEXT | string | "Checksum-Fehler vorhanden" oder "kein Checksum-Fehler vorhanden" |
| STAT_FUNKTIONSFAEHIG | int | "1" wenn Servotronic funktionsfähig |
| STAT_FUNKTIONSFAEHIG_TEXT | string | "Fehler" oder "funktionsfähig" |
| STAT_BETRIEBSZUSTAND | int | 0: Ausgeschaltet 1: Sportkennlinie 2: Komfortkennlinie |
| STAT_BETRIEBSZUSTAND_TEXT | string | Zustand Ausgeschaltet Zustand Sportkennlinie Zustand Komfortkennlinie |
| STAT_ZUSTAND_DIAGLEITUNG | int | 1: SVT-Eigendiagnose aktiv ist high |
| STAT_SOLLSTROM_WERT | int | Sollstrom in mA |
| STAT_SOLLSTROM_EINH | string | "mA" |
| STAT_ISTSTROM_WERT | int | Iststrom in mA |
| STAT_ISTSTROM_EINH | string | "mA" |
| STAT_PWM_AKTUELL_WERT | int | PWM-Verhältnis Highside-Treiber |
| STAT_PWM_AKTUELL_EINH | string | "%" |
| STAT_R_WANDLER_WERT | int | Wertebereich 0 - 25 Ohm, elektrischer Widerstand des Wandlers |
| STAT_R_WANDLER_EINH | string | "Ohm" |
| STAT_KENNLINIE_ORT | string | "Flash" oder "EEPROM" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-status-memory-position-spiegel"></a>
### STATUS_MEMORY_POSITION_SPIEGEL

Abfrage der MemoryPosition der beiden Aussenspiegel KWP2000: $30 InputOutputControlByLocalIdentifier $0A Position Spiegel $01 ReportCurrentState

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MEM_POS | int | 1 bis 254 welche Memoryposition |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MEM_POS_SLOT_WERT | int | abgefragter Memorypositionsslot |
| STAT_MEM_POS_SPIEGEL_FAHRER_HOR_WERT | int | Position Fahrerspiegel horizontal |
| STAT_MEM_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Inkrement, Position Beifahrerspiegel horizontal |
| STAT_MEM_POS_SPIEGEL_FAHRER_VER_WERT | int | Inkrement, Position Fahrerspiegel vertikal |
| STAT_MEM_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Inkrement, Position Beifahrerspiegel vertikal |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-read-vars-comicro"></a>
### _STATUS_READ_VARS_COMICRO

Auslesen der Variablen vom Funktions-Modul Co-Microprozessor KWP2000: $30 InputOutputControlByLocalIdentifier $26 COMICRO_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zentralverriegelung"></a>
### STATUS_ZENTRALVERRIEGELUNG

Auslesen der Variablen vom Funktions-Modul Zentralverriegelung KWP2000: $30 InputOutputControlByLocalIdentifier $27 ZV__VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FA_LOCK_TEXT | string | "ER" wenn Fahrertür entriegelt ist "VR" wenn Fahrertür verriegelt ist "ZS" wenn Fahrertür gesichert ist |
| STAT_BF_LOCK_TEXT | string | "ER" wenn Beifahrertür entriegelt ist "VR" wenn Beifahrertür verriegelt ist "ZS" wenn Beifahrertür gesichert ist |
| STAT_ZV_FA_ENTRIEGELT | unsigned int | 0: Zentralverriegelung Fahrertür NICHT entriegelt 1: Zentralverriegelung Fahrertür entriegelt |
| STAT_ZV_FA_GESICHERT | unsigned int | 0: Zentralverriegelung Fahrertür NICHT gesichert 1: Zentralverriegelung Fahrertür gesichert |
| STAT_ZV_FA_VERRIEGELT | unsigned int | 0: Zentralverriegelung Fahrertür NICHT verriegelt 1: Zentralverriegelung Fahrertür verriegelt |
| STAT_ZV_BF_ENTRIEGELT | unsigned int | 0: Zentralverriegelung Beifahrertür NICHT entriegelt 1: Zentralverriegelung Beifahrertür entriegelt |
| STAT_ZV_BF_GESICHERT | unsigned int | 0: Zentralverriegelung Beifahrertür NICHT gesichert 1: Zentralverriegelung Beifahrertür gesichert |
| STAT_ZV_BF_VERRIEGELT | unsigned int | 0: Zentralverriegelung Beifahrertür NICHT verriegelt 1: Zentralverriegelung Beifahrertür verriegelt |
| STAT_CRASH | int | "1" wenn Crash-Mode aktiv ist |
| STAT_BATTINDEX | int | Rücklesewert des Batterieindex (Spannungsbereich) der Ansteuerung |
| STAT_FA_REPLOCK | int | Zähler der lokalen Wiederholsperre in der Fahrertür |
| STAT_BF_REPLOCK | int | Zähler der lokalen Wiederholsperre in der Beifahrertür |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schlossnuesse"></a>
### STATUS_SCHLOSSNUESSE

Auslesen der Variablen vom Funktions-Modul Schaltnuss KWP2000: $30 InputOutputControlByLocalIdentifier $28 SNU_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SCHLOSSNUSS_1 | int | 0: wenn SNU1 nicht aktiv 1: wenn SNU1 aktiv |
| STAT_SCHLOSSNUSS_2 | int | 0: wenn SNU2 nicht aktiv 1: wenn SNU2 aktiv |
| STAT_SZ_TEXT | string | "NONE" wenn keine gültige Anforderung "ER" wenn Anforderung Entriegeln erkannt "ZS" wenn Anforderung Sichern erkannt |
| STAT_SZ | unsigned int | 0: wenn keine gültige Anforderung 1: wenn Anforderung Entriegeln erkannt 2: wenn Anforderung Sichern erkannt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-buslast"></a>
### STATUS_BUSLAST

Daten zur Buslast KWP2000: $30 InputOutputControlByLocalIdentifier $2A ESL_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_K_CAN | int | Anzahl der K-CAN-Telegramme pro Sekunde |
| STAT_PT_CAN | int | Anzahl der PT-CAN-Telegramme pro Sekunde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bios-virt-sig"></a>
### _STATUS_BIOS_VIRT_SIG

Auslesen der Bussignale KWP2000: $30 InputOutputControlByLocalIdentifier $2B BIOS_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spiegel"></a>
### STATUS_SPIEGEL

Auslesen der Zustände und Variablen vom Modul LIN-Spiegel (Außenspiegel FA/BF) KWP2000: $30 InputOutputControlByLocalIdentifier $24 ASP_VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPIEGEL_FA_TEXT | string | Status Spiegel Fahrerseite "links"  wenn Fahrertür-Spiegel nach links  fährt "oben"   wenn Fahrertür-Spiegel nach oben   fährt "rechts" wenn Fahrertür-Spiegel nach rechts fährt "unten"  wenn Fahrertür-Spiegel nach unten  fährt |
| STAT_SPIEGEL_BF_TEXT | string | Status Spiegel Beifahrerseite "links"  wenn Beifahrertür-Spiegel nach links  fährt "oben"   wenn Beifahrertür-Spiegel nach oben   fährt "rechts" wenn Beifahrertür-Spiegel nach rechts fährt "unten"  wenn Beifahrertür-Spiegel nach unten  fährt |
| STAT_SPIEGEL_FA | unsigned int | Status Spiegel Fahrerseite 0: Ruhestellung 1: Spiegel Fahrerseite nach links 2: Spiegel Fahrerseite nach oben 3: Spiegel Fahrerseite nach rechts 4: Spiegel Fahrerseite nach unten |
| STAT_SPIEGEL_BF | unsigned int | Status Spiegel Beifahrerseite 0: Ruhestellung 1: Spiegel Beifahrerseite nach links 2: Spiegel Beifahrerseite nach oben 3: Spiegel Beifahrerseite nach rechts 4: Spiegel Beifahrerseite nach unten |
| STAT_SPIEGEL_BEIGEKLAPPT_TEXT | string | Aussenspiegel beigeklappt/ausgeklappt nur LIN-Spiegel |
| STAT_SPIEGEL_BEIGEKLAPPT | int | 0: Aussenspiegel ausgeklappt 1: Aussenspiegel beigeklappt nur LIN-Spiegel |
| STAT_LIN_SPIEGEL | unsigned int | "1" wenn LIN-Spiegel verbaut sind |
| STAT_FA_POS_HOR | int | Inkremente für die horizontale Position des Spiegels an der Fahrertür nur LIN-Spiegel |
| STAT_FA_POS_VER | int | Inkremente für die vertikale Position des Spiegels an der Fahrertür nur LIN-Spiegel |
| STAT_BF_POS_HOR | int | Inkremente für die horizontale Position des Spiegels an der Beifahrertür nur LIN-Spiegel |
| STAT_BF_POS_VER | int | Inkremente für die vertikale Position des Spiegels an der Beifahrertür nur LIN-Spiegel |
| STAT_HEIZUNG_EIN | int | Rücklesewert der Spiegelheizung in % |
| STAT_EC | int | eingestellter Verdunkelungsgrad in % nur LIN-Spiegel |
| STAT_WSPERRE_ZAEHLER | int | Wiederholsperrenzähler Spiegelbeiklappen nur LIN-Spiegel |
| STAT_WSPERRE_BEIKLAPP_AKTIV | int | "1" wenn Wiederholsperre Beiklappen aktiv nur LIN-Spiegel |
| STAT_HEIZ_ABSCHALTUNG_EIN | int | "0" keine Unterspannung, Spiegelheizung kann aktiviert werden "1" Unterspannung, Spiegelheizung kann nicht aktiviert werden |
| STAT_HEIZ_ECCOS | int | "0" wenn dauerhafte Heizungsabschaltung für ECCOS-Messung nicht aktiv "1" wenn dauerhafte Heizungsabschaltung für ECCOS-Messung aktiv |
| STAT_MEMPOS | int | Letzte abgerufene/gespeicherte Memory-Position, Werte 0 - 3 nur LIN-Spiegel |
| STAT_MECH_SPIEGEL | int | "1" wenn mechanischer Spiegel verbaut |
| STAT_UNTERSPANNUNG | int | Status Unterspannung für Spiegelverstellung "0" Unterspannung nicht aktiv "1" Unterspannung aktiv nur mechanischer Spiegel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-micropowermodule"></a>
### STEUERN_MICROPOWERMODULE

Vorgabe der Relaiszustaende des MicroPowerModuls KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $03 MPM Outputs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MPM_RELAIS_SCHALTEN | string | Relais ein/aus-schalten,siehe Tabelle STEUERN_MPM Standverbraucher zeitkodiert ausschalten, siehe Tabelle STEUERN_MPM |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-licht"></a>
### STEUERN_LICHT

Vorgabe der Schaltzustaende der Ausstiegsleuchte ASL, Vorfeldbeleuchtung VFB Und LED´s des Schalterblocks KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $04 ESL Outputs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LICHT_SCHALTEN | string | siehe Tabelle STEUERN_LICHT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-spiegel"></a>
### STEUERN_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SPIEGEL | string | table Auswahl_Spiegel NAME TEXT |
| RICHTUNG_SPIEGEL | string | table Richtung_Spiegel NAME TEXT |
| ANSTEUER_ZEIT_SPIEGEL | int | Zeit in 100ms, die der Spiegel angesteuert werden soll, d.h. 1 = 100ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegel-abblenden"></a>
### STEUERN_SPIEGEL_ABBLENDEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel Abblenden der Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGEL_ABBLENDEN_WERT | int | Wert 0 -100%, wie Aussenspiegel abgeblendet werden soll, zb. 40 = 40% Abblendgrad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegelheizung"></a>
### STEUERN_SPIEGELHEIZUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel Spiegelheizung mit speziellen Werten eischalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGELHEIZUNG_WERT | string | Wert fuer Spiegelheizung, siehe Tabelle "Spiegel_Heizung" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-memory-position-spiegel"></a>
### STEUERN_MEMORY_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel Memory Schreiben der MemoryPosition der beiden Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MEM_POS | int | 1 bis 254 welche Memoryposition |
| MEM_POS_SPIEGEL_FAHRER_VER_WERT | int | Inkrement, Position Fahrerspiegel vertikal |
| MEM_POS_SPIEGEL_FAHRER_HOR_WERT | int | Inkrement, Position Fahrerspiegel horizontal |
| MEM_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Inkrement, Position Beifahrerspiegel vertikal |
| MEM_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Inkrement, Position Beifahrerspiegel horizontal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-direkt-spiegel"></a>
### STEUERN_POSITION_DIREKT_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Steuern Spiegel ausgewaehlten Spiegel in angegebene Position fahren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SPIEGEL | string | table Auswahl_Spiegel NAME TEXT Spiegel auswaehlen |
| RICHTUNG_SPIEGEL_HORIZONTAL | int | Inkrement 0 - 254, Absolutwert horizontale Position |
| RICHTUNG_SPIEGEL_VERTIKAL | int | Inkrement 0 - 254, Absolutwert vertikale Position |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-servotronic"></a>
### STEUERN_SERVOTRONIC

Steuerung des Stromwandlers KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $05 SVT Outputs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VORGABE_ART_SERVO_WANDLER | string | "STROM", Steuerung Servo-Wandler über Strom-Vorgabe (in mA, siehe Argument 2) "PWM", Steuerung Servo-Wandler über PWM-Vorgabe (in %, siehe Argument 2) |
| VORGABE_WERT_SERVO_WANDLER | unsigned int | 0-1000 mA bei Strom-Vorgabe 0-100 % bei PWM-Vorgabe |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zentralverriegelung"></a>
### STEUERN_ZENTRALVERRIEGELUNG

Vorgabe der Schaltzustaende der Zentralverriegelung KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTimeAccess $08 ZV__OUTPUTS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZV_SCHALTEN | string | Beide Schlösser entriegeln, verriegeln und sichern Argument siehe Tabelle "STEUERN_ZV" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sitzheizung"></a>
### STEUERN_SITZHEIZUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0D Steuern Sitzheizung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LINDATEN_SEAT_HEAT | string | 4 Byte Daten fuer Sitzheizung, werden einfach durchgereicht |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-historienspeicher-lesen-block-1"></a>
### STATUS_HISTORIENSPEICHER_LESEN_BLOCK_1

EnergieDatenSpeicher Teil 1 -Einschlafverhinderer- auslesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE0 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DATENSATZ_1 | string | "DATENSATZ" |
| STAT_VERURSACHER_1 | int | Des verursachenden Steuergerätes |
| STAT_VERURSACHER_HEX_1 | string | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_1 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_1 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_1 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_2 | string | "DATENSATZ" |
| STAT_VERURSACHER_2 | int | Des verursachenden Steuergerätes |
| STAT_VERURSACHER_HEX_2 | string | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_2 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_2 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_2 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_3 | string | "DATENSATZ" |
| STAT_VERURSACHER_3 | int | Des verursachenden Steuergerätes |
| STAT_VERURSACHER_HEX_3 | string | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_3 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_3 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_3 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_4 | string | "DATENSATZ" |
| STAT_VERURSACHER_4 | int | Des verursachenden Steuergerätes |
| STAT_VERURSACHER_HEX_4 | string | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_4 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_4 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_4 | string | Einheit fuer KM_STAND: KM |
| STAT_DATENSATZ_5 | string | "DATENSATZ" |
| STAT_VERURSACHER_5 | int | Des verursachenden Steuergerätes |
| STAT_VERURSACHER_HEX_5 | string | Des verursachenden Steuergerätes |
| STAT_RELATIVZEIT_WERT_5 | unsigned long | Kombi Relativzeit bei Abspeicherung [s] |
| STAT_RELATIVZEIT_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_KM_STAND_WERT_5 | unsigned long | Der aktuelle km_Stand [Km] |
| STAT_KM_STAND_EINH_5 | string | Einheit fuer KM_STAND: KM |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-historienspeicher-lesen-block-2"></a>
### STATUS_HISTORIENSPEICHER_LESEN_BLOCK_2

EnergieDatenSpeicher Teil 2 -Wecker- aus lesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE1 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DATENSATZ_0 | string | "DATENSATZ" |
| STAT_RELATIVZEIT_BEGINN_WERT_0 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_RELATIVZEIT_BEGINN_EINH_0 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_GESAMTE_KM_WERT_0 | unsigned long | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_ANZAHL_FAHRTEN_0_5_KM_0 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_0 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_0 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_0 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_GESAMTE_KM_EINH_0 | string | Einheit fuer KM_STAND: KM |
| STAT_ANZAHL_FAHRTEN_WECKER_0 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_1 | string | "DATENSATZ" |
| STAT_GESAMTE_KM_EINH_1 | string | Einheit fuer KM_STAND: KM |
| STAT_RELATIVZEIT_BEGINN_EINH_1 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_BEGINN_WERT_1 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_GESAMTE_KM_WERT_1 | unsigned long | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_ANZAHL_FAHRTEN_0_5_KM_1 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_1 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_1 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_1 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_1 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_2 | string | "DATENSATZ" |
| STAT_GESAMTE_KM_EINH_2 | string | Einheit fuer KM_STAND: KM |
| STAT_RELATIVZEIT_BEGINN_EINH_2 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_BEGINN_WERT_2 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_GESAMTE_KM_WERT_2 | unsigned long | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_ANZAHL_FAHRTEN_0_5_KM_2 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_2 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_2 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_2 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_2 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_3 | string | "DATENSATZ" |
| STAT_GESAMTE_KM_EINH_3 | string | Einheit fuer KM_STAND: KM |
| STAT_RELATIVZEIT_BEGINN_EINH_3 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_BEGINN_WERT_3 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_GESAMTE_KM_WERT_3 | unsigned long | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_ANZAHL_FAHRTEN_0_5_KM_3 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_3 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_3 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_3 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_3 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_4 | string | "DATENSATZ" |
| STAT_GESAMTE_KM_EINH_4 | string | Einheit fuer KM_STAND: KM |
| STAT_RELATIVZEIT_BEGINN_EINH_4 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_BEGINN_WERT_4 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_GESAMTE_KM_WERT_4 | unsigned long | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_ANZAHL_FAHRTEN_0_5_KM_4 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_4 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_4 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_4 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_4 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| STAT_DATENSATZ_5 | string | "DATENSATZ" |
| STAT_GESAMTE_KM_EINH_5 | string | Einheit fuer KM_STAND: KM |
| STAT_RELATIVZEIT_BEGINN_EINH_5 | string | Einheit fuer RELATIVZEIT: SEKUNDEN |
| STAT_RELATIVZEIT_BEGINN_WERT_5 | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] |
| STAT_GESAMTE_KM_WERT_5 | unsigned long | Gefahrene Km über den Aufzeichnungszeitraum [Km] |
| STAT_ANZAHL_FAHRTEN_0_5_KM_5 | int | Anzahl Fahrten 0..5 Km [Km] |
| STAT_ANZAHL_FAHRTEN_5_20_KM_5 | int | Anzahl Fahrten 6..20 Km [Km] |
| STAT_ANZAHL_FAHRTEN_20_100_KM_5 | int | Anzahl Fahrten 21..100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_UEBER_100_KM_5 | int | Anzahl Fahrten &gt;100 Km [Km] |
| STAT_ANZAHL_FAHRTEN_WECKER_5 | int | Die maximale Anzahl Wecker zwischen zwei Klemmenzuständen, KLR ein aufzuzeichnen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-historienspeicher-lesen-block-3"></a>
### STATUS_HISTORIENSPEICHER_LESEN_BLOCK_3

EnergieDatenSpeicher Teil 3 - Wecker-ID - auslesen KWP 2000: $22   ReadDataByCommonIdentifier KWP 2000: $EFE2 commonProjectSpecific

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WECKER_CAN_ID | unsigned int | ID (dez.) des verursachenden Steuergerätes Die 26 Einträge werden auf die Results STAT_WECKER_CAN_ID_xx (xx = 0,1,2,...) abgebildet |
| STAT_WECKER_CAN_ID_HEX | string | ID (hex.) des verursachenden Steuergerätes Die 26 Einträge werden auf die Results STAT_WECKER_CAN_ID_HEX_xx (xx = 0,1,2,...) abgebildet |
| STAT_WECKER_SG_ANZAHL | int | Anzahl der möglichen Sender für dieses CAN ID Die 26 Einträge werden auf die Results STAT_WECKER_SG_ANZAHL_xx (xx = 0,1,2,...) abgebildet |
| STAT_WECKER_SG_ID | unsigned int | Diagnoseadresse des Senders für dieses CAN ID Die 26 Einträge werden auf die Results STAT_WECKER_SG_ID_xx (xx = 0,1,2,...) abgebildet Je nach Anzahl der möglichen Sender für dieses CAN-ID (i = 1,2,...) existieren i mal folgende Results: (unsigned int)    STAT_WECKER_SG_ID_xx_i   dez. Diagnoseadresse des Senders i |
| STAT_WECKER_SG_ID_HEX | string | Diagnoseadresse des Senders für dieses CAN ID Die 26 Einträge werden auf die Results STAT_WECKER_SG_ID_HEX_xx (xx = 0,1,2,...) abgebildet Je nach Anzahl der möglichen Sender für dieses CAN-ID (i = 1,2,...) existieren i mal folgende Results: (string) STAT_WECKER_SG_ID_HEX_xx_i   hex. Diagnoseadresse des Senders i |
| STAT_WECKER_SG_NAME | string | Name des Senders für dieses CAN ID Die 26 Einträge werden auf die Results STAT_WECKER_SG_NAME_xx (xx = 0,1,2,...) abgebildet Je nach Anzahl der möglichen Sender für dieses CAN-ID (i = 1,2,...) existieren i mal folgende Results: (string) STAT_WECKER_SG_NAME_xx_i   Name des Senders i |
| STAT_RELATIVZEIT_BEGINN_WERT | unsigned long | Relativzeit zu Beginn der Aufzeichung [s] Die 26 Einträge werden auf die Results STAT_RELATIVZEIT_BEGINN_WERT_xx (xx = 0,1,2,...) abgebildet |
| STAT_KM_STAND_WERT | unsigned long | Der aktuelle km_Stand [km] Die 26 Einträge werden auf die Results STAT_KM_STAND_WERT_xx (xx = 0,1,2,...) abgebildet |
| STAT_RELATIVZEIT_EINH | string | Einheit fuer RELATIVZEIT (alle Einträge): SEKUNDEN |
| STAT_KM_STAND_EINH | string | Einheit fuer KM_STAND (alle Einträge): KM |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-historienspeicher-loeschen"></a>
### STEUERN_HISTORIENSPEICHER_LOESCHEN

EnergieDatenSpeicher loeschen KWP 2000: $22   WriteDataByCommonIdentifier KWP 2000: $EFE3 commonProjectSpecific

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FDM_BLOCK | int | " 1 " , um Datensatz Teil 1 "Einschlafverhinderer" zu löschen " 2 " , um Datensatz Teil 2 "Wecker" zu löschen " 3 " , um Datensatz Teil 3 "Wecker-ID" zu löschen ohne Argument, um alle Datensätze zu löschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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

<a id="job-brif-schreiben-lear"></a>
### _BRIF_SCHREIBEN_LEAR

Beschreiben der BRIF-Inhalte KWP 2000: $3B ApplDiagWriteDataByLocalIdentifier Modus   : 0x70 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BRIF_DATEI | string | Dateiname mit Default-Codierdaten fuer 3900-Bereich Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lear-prod-daten-schreiben"></a>
### _LEAR_PROD_DATEN_SCHREIBEN

Beschreiben von Teilen des BRIF, laufenden SG-Nur., Produktionsdatum Es muessen immer alle Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $3B WriteDataByCommonIdentifier $70 BRIF schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SSECUSN_BYTE_1 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_2 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_3 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_4 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_5 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_6 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_7 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_8 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| SSECUSN_BYTE_9 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| DOECUM_BYTE_1 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| DOECUM_BYTE_2 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| DOECUM_BYTE_3 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| DOECUM_BYTE_4 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| HW_INDEX_X | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-lesen"></a>
### _HERSTELLERDATEN_LESEN

Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $72 Herstellerdaten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE_1 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_2 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_3 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_4 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_5 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_6 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_7 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_8 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_9 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_10 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-schreiben"></a>
### _HERSTELLERDATEN_SCHREIBEN

Beschreiben der Herstellerdaten Es muessen immer alle Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $3B WriteDataByCommonIdentifier $71 Herstellerdaten Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_1 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_2 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_3 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_4 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_5 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_6 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_7 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_8 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_9 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE_10 | unsigned char | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-linkinfo-gwversion-lesen"></a>
### _LINKINFO_GWVERSION_LESEN

Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $73 LinkInfo Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| LINKDATUM_TAG | string |  |
| LINKDATUM_MONAT | string |  |
| LINKDATUM_JAHR | string |  |
| LINKDATUM_UHRZEIT | string |  |
| GW_VERSION | string | Version der Gateway-Tabelle |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-kgm-send-message"></a>
### _KGM_SEND_MESSAGE

Auslesen der Stati von den digitalen Eingaengen KWP2000: $31 StartRoutineByLocalIdentifier $11 CommonSwitch

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAN_SELECTION | unsigned int | "1" fuer K_CAN, oder "2" fuer PT_CAN |
| ECU_ADRESS | unsigned int | SG-Adresse, zB. 0x0600 für KGM |
| MESSAGE_DLC | unsigned int | Telegramm-Länge |
| DATABYTE_1 | unsigned int |  |
| DATABYTE_2 | unsigned int |  |
| DATABYTE_3 | unsigned int |  |
| DATABYTE_4 | unsigned int |  |
| DATABYTE_5 | unsigned int |  |
| DATABYTE_6 | unsigned int |  |
| DATABYTE_7 | unsigned int |  |
| DATABYTE_8 | unsigned int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fensterheber"></a>
### STATUS_FENSTERHEBER

Stati der einzelnen FH-Funktionen auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FA_FH_OFFEN_KOMPLETT | int | Fensterheber Fahrer komplett offen |
| STAT_BF_FH_OFFEN_KOMPLETT | int | Fensterheber Beifahrer komplett offen |
| STAT_FA_FH_GESCHLOSSEN | int | Fensterheber Fahrer geschlossen |
| STAT_BF_FH_GESCHLOSSEN | int | Fensterheber Beifahrer geschlossen |
| STAT_FA_FH_FAEHRT_EIN | int | Fensterheber Fahrer faehrt |
| STAT_FA_FH_FAEHRT_AUF_EIN | int | Fensterheber Fahrer faehrt auf |
| STAT_FA_FH_FAEHRT_ZU_EIN | int | Fensterheber Fahrer faehrt zu |
| STAT_BF_FH_FAEHRT_EIN | int | Fensterheber Beifahrer faehrt |
| STAT_BF_FH_FAEHRT_AUF_EIN | int | Fensterheber Beifahrer faehrt auf |
| STAT_BF_FH_FAEHRT_ZU_EIN | int | Fensterheber Beifahrer faehrt zu |
| STAT_FA_FH_EINGELERNT_EIN | int | Fensterheber Fahrer eingelernt |
| STAT_BF_FH_EINGELERNT_EIN | int | Fensterheber Beifahrer eingelernt |
| STAT_FA_FH_THERMOSCHUTZ | int | Fensterheber Fahrer Thermoschutz Status |
| STAT_BF_FH_THERMOSCHUTZ | int | Fensterheber Beifahrer Thermoschutz Status |
| STAT_FA_FH_THERMOSCHUTZ_TEXT | string | Fensterheber Fahrer Thermoschutz Bedeutung |
| STAT_BF_FH_THERMOSCHUTZ_TEXT | string | Fensterheber Beifahrer Thermoschutz Bedeutung |
| STAT_FA_FH_POSITION_WERT | int | Position Fensterheber Fahrer, nur bei eingelerntem FH |
| STAT_BF_FH_POSITION_WERT | int | Position Fensterheber Beifahrer, nur bei eingelerntem FH |
| STAT_FH_TASTERBF_BF_ZU | unsigned int | Beifahrerseite (lokaler Taster): Fensterheber Beifahrerseite ZU (Fenster schliessen) UNTERSTUETZT AB 03/2006 !! 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERBF_BF_AUF | unsigned int | Beifahrerseite (lokaler Taster): Fensterheber Beifahrerseite AUF (Fenster oeffnen) UNTERSTUETZT AB 03/2006 !! 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERBF_BF_MAUT_ZU | unsigned int | Beifahrerseite (lokaler Taster): Fensterheber Beifahrerseite MAUT ZU (Fenster komplett schliessen) UNTERSTUETZT AB 03/2006 !! 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERBF_BF_MAUT_AUF | unsigned int | Beifahrerseite (lokaler Taster): Fensterheber Beifahrerseite MAUT AUF (Fenster oeffnen) UNTERSTUETZT AB 03/2006 !! 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERBF_BF_GESAMT | string | Beifahrerseite (lokaler Taster): Fensterheber Beifahrerseite gesamt UNTERSTUETZT AB 03/2006 !! 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-status-fh-adaptionswerte"></a>
### _STATUS_FH_ADAPTIONSWERTE

Die Adaptionswerte sind ein Maß der mechanischen Güte des FH-Antriebs Auswertung grafisch linear (f-&gt;f(x), x = Byteposition, f = Bytewert) Modus  : Default KWP2000: $22 ReadDataByCommonIdentifier $37xx Speicherdaten je nach FH-Seite

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | table Auswahl_Fenster NAME TEXT Auswahl des Fensterhebers, dessen Adaptionswerte ausgelesen werden soll: "FH_FA" für Fahrer, "FH_BF" für Beifahrer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ADAPTIONSWERTE | binary | Adaptionswerte des ausgewählten FH |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-denorm-logger-loeschen"></a>
### STATUS_FH_DENORM_LOGGER_LOESCHEN

Denormierungslogger löschen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $07 ShortTimeAccess

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_LOGGER | unsigned char | "1" fuer Denormierungslogger "2" fuer Reversierungslogger |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-denormierer"></a>
### STATUS_FH_LOGGER_DENORMIERER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen der letzten drei Einträge von EE_FH_LOG_DATA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-denormierungs-logger-lesen"></a>
### _STATUS_FH_DENORMIERUNGS_LOGGER_LESEN

Fensterheber Denorierungslogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReadCurrentState $14 SUBSWITCH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-reversierer"></a>
### STATUS_FH_LOGGER_REVERSIERER

Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReadCurrentState $16 SUBSWITCH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REVERSIERUNGS_COUNTER | unsigned int | absolute Zahl der Reversierer, 0 - 65535 |
| STAT_DATENSATZ_1 | string | Nummer des letzten Datensatzes |
| STAT_FEHLERNUMMER_1 | int | Fehlernummer des letzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_1 | string | Fehlertext des letzten Reversierers |
| STAT_HEADER_1 | int | Detailinformation zum Fehler des letzten Reversierers |
| STAT_HEADER_TEXT_1 | string | Text zur Detailinformation zum Fehler des letzten Reversierers |
| STAT_POSITION_HZ_1 | int | Scheibenposition in Hallsignale beim letzten Reversierer |
| STAT_MOTOR_1 | int | Status des Motors (Flags) beim letzten Reversierer |
| STAT_IN_VOLTAGE_WERT_1 | real | Spannung am Fensterheber-Relais beim letzten Reversierer |
| STAT_VOLTAGE_WERT_1 | real | Fensterheberspannung beim letzten Reversierer |
| STAT_SPEED_WERT_1 | real | Fahrzeuggeschwindigkeit in km/h beim letzten Reversierer |
| STAT_AUSSENTEMP_WERT_1 | real | Aussentemperatur in °C beim letzten Reversierer |
| STAT_TOPSTATUS_1 | int | Details hierzu liegen bei Fa. Brose |
| STAT_DATENSATZ_2 | string | Nummer des vorletzten Datensatzes |
| STAT_FEHLERNUMMER_2 | int | Fehlernummer des vorletzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_2 | string | Fehlertext des vorletzten Reversierers |
| STAT_HEADER_2 | int | Detailinformation zum Fehler des vorletzten Reversierers |
| STAT_HEADER_TEXT_2 | string | Text zur Detailinformation zum Fehler des vorletzten Reversierers |
| STAT_POSITION_HZ_2 | int | Scheibenposition in Hallsignale beim vorletzten Reversierer |
| STAT_MOTOR_2 | int | Status des Motors (Flags) beim vorletzten Reversierer |
| STAT_IN_VOLTAGE_WERT_2 | real | Spannung am Fensterheber-Relais beim vorletzten Reversierer |
| STAT_VOLTAGE_WERT_2 | real | Fensterheberspannung beim vorletzten Reversierer |
| STAT_SPEED_WERT_2 | real | Fahrzeuggeschwindigkeit in km/h beim vorletzten Reversierer |
| STAT_AUSSENTEMP_WERT_2 | real | Aussentemperatur in °C beim vorletzten Reversierer |
| STAT_TOPSTATUS_2 | int | Details hierzu liegen bei Fa. Brose |
| STAT_DATENSATZ_3 | string | Nummer des drittletzten Datensatzes |
| STAT_FEHLERNUMMER_3 | int | Fehlernummer des drittletzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_3 | string | Fehlertext des drittletzten Reversierers |
| STAT_HEADER_3 | int | Detailinformation zum Fehler des drittletzten Reversierers |
| STAT_HEADER_TEXT_3 | string | Text zur Detailinformation zum Fehler des drittletzten Reversierers |
| STAT_POSITION_HZ_3 | int | Scheibenposition in Hallsignale beim drittletzten Reversierer |
| STAT_MOTOR_3 | int | Status des Motors (Flags) beim drittletzten Reversierer |
| STAT_IN_VOLTAGE_WERT_3 | real | Spannung am Fensterheber-Relais beim drittletzten Reversierer |
| STAT_VOLTAGE_WERT_3 | real | Fensterheberspannung beim drittletzten Reversierer |
| STAT_SPEED_WERT_3 | real | Fahrzeuggeschwindigkeit in km/h beim drittletzten Reversierer |
| STAT_AUSSENTEMP_WERT_3 | real | Aussentemperatur in °C beim drittletzten Reversierer |
| STAT_TOPSTATUS_3 | int | Details hierzu liegen bei Fa. Brose |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-reversierungs-logger-lesen"></a>
### _STATUS_FH_REVERSIERUNGS_LOGGER_LESEN

Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $25 FH__VAR_READ $01 ReadCurrentState $16 SUBSWITCH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REVERSIERUNGS_COUNTER | unsigned int | absolute Zahl der Reversierer, 0 - 65535 |
| STAT_DATENSATZ | string | Datensatz Nummer |
| STAT_FEHLERNUMMER | int | Fehlernummer des Reversierers |
| STAT_FEHLERNUMMER_TEXT | string | Fehlertext des Reversierers |
| STAT_HEADER | int | Detailinformation zum Fehler |
| STAT_HEADER_TEXT | string | Text zur Detailinformation |
| STAT_POSITION_HZ | int | Scheibenposition in Hallsignale |
| STAT_MOTOR | int | Status des Motors (Flags) |
| STAT_IN_VOLTAGE_WERT | real | Spannung am Fensterheber-Relais |
| STAT_VOLTAGE_WERT | real | Fensterheberspannung |
| STAT_SPEED_WERT | real | Fahrzeuggeschwindigkeit in km/h |
| STAT_AUSSENTEMP_WERT | real | Aussentemperatur in °C |
| STAT_TOPSTATUS | int | Details hierzu liegen bei Fa. Brose |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-diagnose-brose"></a>
### _STEUERN_FENSTERHEBER_DIAGNOSE_BROSE

KWP2000: $30 InputOutputControlByLocalIdentifier $07 Diagnose Jobs 1-5 fuer BROSE-FH $07 ShortTermAdjustment Status von KGM schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_JOB | unsigned char | "1" fuer Job 1,..., "5" fuer Job 5 |
| BYTE_1 | unsigned char |  |
| BYTE_2 | unsigned char |  |
| BYTE_3 | unsigned char |  |
| BYTE_4 | unsigned char |  |
| BYTE_5 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-mit-eks-einlernen"></a>
### STEUERN_FENSTERHEBER_MIT_EKS_EINLERNEN

Einlernen der Fensterheber mit Einklemmschutz (EKS) KWP2000: $30 InputOutputControlByLocalIdentifier $07 Ansteuern FH $07 ShortTermAdjustment Dauer max. 14sec

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HUBLAENGE_FH_FAT | unsigned int | Hublaenge über den kompl. Verfahrweg des FH-Fahrertuer bei 0 wird der FH nicht eingelernt Weginkrement, Bereich von 1100 - 1300 wird kein Argument angegeben so wird die codierte Hublaenge verwendet |
| HUBLAENGE_FH_BFT | unsigned int | Hublaenge über den kompl. Verfahrweg des FH-Beifahrertuer bei 0 wird der FH nicht eingelernt Weginkrement, Bereich von 1100 - 1300 wird kein Argument angegeben so wird die codierte Hublaenge verwendet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-denormieren"></a>
### STEUERN_FENSTERHEBER_DENORMIEREN

Denormieren der Fensterheber, je nach Auswahl Fahrer, Beifahrer, beide KWP2000: $30 InputOutputControlByLocalIdentifier $07 Ansteuern FH $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | table Auswahl_Fenster NAME TEXT Auswahl des Fensterhebers, der denormiert werden soll: FH_FA für Fahrer, FH_BF für Beifahrer, BEIDE_FH für beide |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber"></a>
### STEUERN_FENSTERHEBER

Ansteuerung des Fensterhebers an der Fahrertuer (FA) und/oder der Beifahrertuer (BF) KWP2000: $30 InputOutputControlByLocalIdentifier $07 Steuern Fensterheber $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | int | Gibt die Art der Ansteuerung für die Fensterheber an = Zahlenwert der Spalte ARGUMENT aus Tabelle STEUERN_FH_FAT_BFT: Die Bedeutung von ELEMENT steht in Spalte NAME und BESCHREIBUNG |
| AKTION | int | Ansteuerzeit für die Fensterheber-Motoren: 0 - 100 Zeitangabe in 100ms-Schritten = 0 - 10s Ansteuerzeit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-ohne-eks"></a>
### _STEUERN_FENSTERHEBER_OHNE_EKS

Ansteuerung des Fensterhebers an beiden Tueren ACHTUNG: Einklemmschutz ABGESCHALTET, keine Normierung erforderlich KWP2000: $30 InputOutputControlByLocalIdentifier $07 Steuern Fensterheber $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LAUFZEIT_FAT | int | Ansteuerzeit für den Fensterheber Fahrertuer: (-100) - (+100) Zeitangabe in 100ms-Schritten = 0 - 10s Ansteuerzeit Richtung über Vorzeichen: positiv=oeffnen, negativ=schliessen |
| LAUFZEIT_BFT | int | Ansteuerzeit für den Fensterheber Beifahrertuer: (-100) - (+100) Zeitangabe in 100ms-Schritten = 0 - 10s Ansteuerzeit Richtung über Vorzeichen: positiv=oeffnen, negativ=schliessen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fh-fat-kurzhub-init-lear"></a>
### _FH_FAT_KURZHUB_INIT_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fh-bft-kurzhub-init-lear"></a>
### _FH_BFT_KURZHUB_INIT_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fh-init-dichtung-lear"></a>
### _STEUERN_FH_INIT_DICHTUNG_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INIT_FAT_DICHTUNG | int | von 0 - 254 Anzahl von FH-Hub ohne Softclose |
| INIT_BFT_DICHTUNG | int | von 0 - 254 Anzahl von FH-Hub ohne Softclose |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-init-dichtung-lear"></a>
### _STATUS_FH_INIT_DICHTUNG_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $3930 Codierdaten aus Info-Block Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INIT_DICHTUNG_FAT | unsigned int | Zähler der restlichen Schließvorgänge ohne Sanfteinlauf an der FAT |
| STAT_INIT_DICHTUNG_BFT | unsigned int | Zähler der restlichen Schließvorgänge ohne Sanfteinlauf an der BFT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-laderaumabdeckung"></a>
### STATUS_LADERAUMABDECKUNG

Status der Laderaumabdeckung (Lara CRoFt) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2C LARA_VAR_READ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LARA_APPL_STATE | int | SW-Status allgemein |
| STAT_LARA_APPL_MOTORSTATE | int | SW-Status Antrieb |
| STAT_LARA_APPL_TIMEOUT | int | Anzeige SW-Timeout (1 = aktiv) |
| STAT_LARA_APPL_REPEATLOCK | int | Anzeige Wiederholsperre (1 = aktiv) |
| STAT_LARA_APPL_HKK | int | Status Heckklappenkontakt |
| STAT_LARA_APPL_HSK | int | Status Heckscheibenkontakt |
| STAT_LARA_APPL_HKLIFT | int | Status Heckklappenlift |
| STAT_LARA_APPL_REEDCONTACT | int | Rollo am Reedkontakt erkannt |
| STAT_LARA_APPL_COVERCLOSED | int | Rollo geschlossen |
| STAT_LARA_APPL_REVERSED | int | Antrieb reversiert nach Einklemmen |
| STAT_LARA_APPL_UPPEREND | int | Rollo am oberen Anschlag |
| STAT_LARA_APPL_LOWEREND | int | Rollo am unteren Anschlag |
| STAT_LARA_APPL_FETRAWE | int | FeTraWe aktiviert (Funktion deaktiviert) |
| STAT_LARA_APPL_NEWSTATE | int | neuer SW-Zustand erreicht |
| STAT_LARA_APPL_LARA_ACTIVE | int | Laderaumabdeckung aktiv |
| STAT_LARA_LCPA_DENORMED | int | Laderaumabdeckung (LCPA) denormiert, keine Fahrt nach unten moeglich |
| STAT_LARA_APPL_REPLOCKCOUNTER | unsigned long | Wiederholzaehler |
| STAT_LARA_APPL_TIMEOUTCOUNTER | unsigned long | Timeoutzaehler der Applikation |
| STAT_LARA_COUNTER_TOTAL_CYCLES | unsigned int | Dauerzähler: gesamte Zyklen (Fahrten / 2) |
| STAT_LARA_COUNTER_TOTAL_REVERSES | unsigned int | Dauerzähler: gesamte Reversierungen |
| STAT_LARA_COUNTER_TOTAL_BLOCKS | unsigned int | Dauerzähler: gesamte Blockfahrten |
| STAT_LARA_COUNTER_TOTAL_NORMS | unsigned int | Dauerzähler: gesamte verlorene Normierungen |
| STAT_LARA_COUNTER_CYCLIC_NORMS | unsigned int | variabler Down-Zähler: Fahrten bis nächster Normierung errechnet sich aus Gesamtzyklen modulo Normierzahl |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-laderaumabdeckung"></a>
### STEUERN_LADERAUMABDECKUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0C Steuern Laderaumabdeckung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_STELLUNG | string | Ziel als String aus Tabelle Steuern_LARA_POS Spalte NAME oder numerischer Wert für Zielposition nach unten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lara-lear"></a>
### _STEUERN_LARA_LEAR

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0C Steuern Laderaumabdeckung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_RICHTUNG | int | "1" für nach unten, "2" für nach oben |
| AUSWAHL_MODE | int | "2" für Laderaum-LCPA, andere Modi zulässig (1-6) |
| AUSWAHL_ENDANSCHLAG | int | "1" für Endanschlagerkennung LCPA, andere Einstellungen zulässig (0-2) |
| POSITION_LADERAUMABDECKUNG | unsigned int | Zielposition 0-5000, sinnvoll für Lara: 0 (=oben) bis 454 (=unten) |
| LINDATEN_LARA | string | 4 Byte Daten fuer Lara, werden einfach durchgereicht LINDATEN überschreiben die vorherigen Werte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lara-counter-reset"></a>
### _LARA_COUNTER_RESET

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default KWP2000: $2E WriteDataByCommonIdentifier Kodierblock lesen, verändern, zurückschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LARA_COUNTER | string | Welche(r) Block soll gelöscht werden "BLOCKS","REVERSES","NORMS","ALL" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codieren-lcpa"></a>
### _CODIEREN_LCPA

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0e CODIEREN LCPA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_LCPA | string | 4 Byte Daten fuer Kodierung, werden einfach durchgereicht |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cks-lcpa"></a>
### _CKS_LCPA

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0e CKS LCPA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CKS_DATEN_LCPA | string | 4 Byte Daten fuer CKS, werden einfach durchgereicht |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-lcpa-ident"></a>
### READ_LCPA_IDENT

ident lesen des LIN-Slave CPA Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-LCPA Modus  : Default Auslesen der Identdaten der LCPA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_VERSION_LCPA | string | SW-Version fuer LCPA |
| ID_BMW_NR_LCPA | string | BMW_Teilenummer fuer das LCPA |
| CODING_INDEX_LCPA | string | Codierindex fuer LCPA |
| MCV_VERSION_LCPA | string | Nummer Nachrichtenkatalog fuer das LCPA |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben-lcpa"></a>
### C_FG_SCHREIBEN_LCPA

Schreiben der FG-Nr. in den LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_LCPA | string | Fahrgestellnummer LCPA (18-stellig) |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen-lcpa"></a>
### C_FG_LESEN_LCPA

Lesen der FG-Nr. aus dem LCPA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_LCPA | string | Fahrgestellnummer (7-stellig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag-lcpa"></a>
### C_FG_AUFTRAG_LCPA

Schreiben und Lesen der FG-Nr. LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_LCPA | string | Fahrgestellnummer LCPA (18-stellig) |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben-lcpa"></a>
### C_AEI_SCHREIBEN_LCPA

Schreiben des Aenderungsindex in den LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AEI_LCPA | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen-lcpa"></a>
### C_AEI_LESEN_LCPA

Lesen des Aenderungsindex aus dem LCPA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AEI_LCPA | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag-lcpa"></a>
### C_AEI_AUFTRAG_LCPA

Schreiben und Lesen des Aenderungsindex LCPA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AEI_LCPA | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-lcpa"></a>
### RESET_LCPA

Reset LCPA KWP2000: $A6 LINGateway $11 Reset

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAD | int | NAD des gewuenschten LIN-Teilnehmers Wenn nicht angegeben, wird 0xCA für das LCPA angenommen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (46 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (23 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (9 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (17 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (11 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (7 × 9)
- [AUSWAHL_SPIEGEL](#table-auswahl-spiegel) (3 × 3)
- [RICHTUNG_SPIEGEL](#table-richtung-spiegel) (7 × 3)
- [SPIEGEL_HEIZUNG](#table-spiegel-heizung) (11 × 3)
- [STEUERN_SERVOTRONIC](#table-steuern-servotronic) (3 × 3)
- [AUSWAHL_FENSTER](#table-auswahl-fenster) (4 × 3)
- [STEUERN_MPM](#table-steuern-mpm) (4 × 3)
- [STEUERN_LICHT](#table-steuern-licht) (9 × 3)
- [STEUERN_ZV](#table-steuern-zv) (5 × 3)
- [STEUERN_LARA_POS](#table-steuern-lara-pos) (7 × 6)
- [STEUERN_FH_FAT_BFT](#table-steuern-fh-fat-bft) (13 × 3)
- [FH_DENORM_FEHLERTEXTE](#table-fh-denorm-fehlertexte) (26 × 2)
- [FH_REVERSIER_FEHLERTEXTE](#table-fh-reversier-fehlertexte) (8 × 2)
- [ZUORDNUNG_CAN_ID_SG](#table-zuordnung-can-id-sg) (409 × 6)

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

Dimensions: 46 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC904 | CAN-Low, Physikalischer Fehler |
| 0xC905 | CAN-High, Kurzschluss VB |
| 0xC906 | Ground Shift, zu hoch |
| 0xC907 | Controller K-CAN, Bus Off |
| 0xC908 | Controller PT-CAN, Bus Off |
| 0x93A8 | interner Fehler |
| 0x93A9 | Klemme 30A Anschluss fehlerhaft |
| 0x93AA | Klemme 30B Anschluss fehlerhaft |
| 0x93AB | Relaiskleber MPM-Relais ein |
| 0x93AC | Relaiskleber MPM-Relais aus |
| 0x93AD | MPM kein SVIN |
| 0x93AE | Hallsensor FH-Fahrertuer defekt |
| 0x93AF | Hallsensor FH-Beifahrertuer defekt |
| 0x93B0 | Relais FH-Fahrertuer defekt |
| 0x93B1 | Relais FH-Beifahrertuer defekt |
| 0x93B2 | Spiegelheizung Fahrerseite defekt |
| 0x93B3 | Antrieb Spiegel Fahrerseite defekt |
| 0x93B4 | Antrieb Beiklappen Spiegel Fahrerseite defekt |
| 0x93B5 | Spiegelheizung Beifahrerseite defekt |
| 0x93B6 | Antrieb Spiegel Beifahrerseite defekt |
| 0x93B7 | Antrieb Beiklappen Spiegel Beifahrerseite defekt |
| 0x93B8 | Servotronik: Timeout Klemmentelegramm |
| 0x93B9 | Servotronik: Klemme 15 ungueltig |
| 0x93BA | Servotronik: Motortimeout |
| 0x93BB | Servotronik: Motorstatus ungueltig |
| 0x93BC | Servotronik: DSC Telegrammtimeout |
| 0x93BD | Servotronik: Geschwindigkeit ungueltig |
| 0x93BE | Servotronik: Klemme 30A fehlt |
| 0x93BF | Servotronik: FDC Timeout |
| 0x93C0 | Servotronik: FDC-Modus ungueltig |
| 0x93C1 | Servotronik: Hardware defekt |
| 0x93C2 | Schaltnuss: Kontakt defekt |
| 0x93C3 | Zentralverriegelung: Kurzschluss Leitung ZV_MER |
| 0x93C4 | Zentralverriegelung: Kurzschluss Leitung ZV_MVFRT |
| 0x93C5 | Zentralverriegelung: Kurzschluss Leitung ZV_MVR |
| 0x93C6 | Zentralverriegelung: Kurzschluss Leitung ZV_MZS |
| 0x93C7 | Klemme 30 Anschluss fehlerhaft |
| 0x93C8 | LCPA Fehler Motorsensor |
| 0x93C9 | keine LIN-Kommunikation zum Spiegel Fahrerseite |
| 0x93CA | keine LIN-Kommunikation zum Spiegel Beifahrerseite |
| 0x93CB | keine LIN-Kommunikation zum Schalterblock |
| 0x93CC | keine LIN-Kommunikation zum LCPA |
| 0x93CD | keine LIN-Kommunikation zur Sitzheizung Fahrerseite |
| 0x93CE | keine LIN-Kommunikation zur Sitzheizung Beifahrerseite |
| 0x93E7 | Energiesparmode aktiv |
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

Dimensions: 23 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x93A8 | 0x01 | 0x05 | - | - |
| 0x93A9 | 0x01 | 0x03 | - | - |
| 0x93AA | 0x01 | 0x03 | - | - |
| 0x93B2 | 0x05 | 0x03 | - | - |
| 0x93B3 | 0x05 | 0x03 | - | - |
| 0x93B4 | 0x05 | 0x03 | - | - |
| 0x93B5 | 0x05 | 0x03 | - | - |
| 0x93B6 | 0x05 | 0x03 | - | - |
| 0x93B7 | 0x05 | 0x03 | - | - |
| 0x93C2 | 0x01 | 0x03 | - | - |
| 0x93C3 | 0x08 | 0x08 | - | - |
| 0x93C4 | 0x08 | 0x08 | - | - |
| 0x93C5 | 0x08 | 0x08 | - | - |
| 0x93C6 | 0x08 | 0x08 | - | - |
| 0x93C7 | 0x01 | 0x03 | - | - |
| 0x93C8 | 0x05 | 0x01 | - | - |
| 0x93C9 | 0x01 | 0x03 | - | - |
| 0x93CA | 0x01 | 0x03 | - | - |
| 0x93CB | 0x01 | 0x03 | - | - |
| 0x93CC | 0x01 | 0x03 | - | - |
| 0x93CD | 0x01 | 0x03 | - | - |
| 0x93CE | 0x01 | 0x03 | - | - |
| default | 0x03 | 0x03 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x02 | Sensorspannung | Volt | - | unsigned char | - | 5 | 255 | 0 |
| 0x03 | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | Geschwindigkeit | km/h | - | unsigned char | - | 10 | 1 | 0 |
| 0x05 | Fehler zusatzinfo | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Zeit 1 | sec | - | unsigned char | - | 256 | 1 | 0 |
| 0x07 | Zeit 2 | sec | - | unsigned char | - | 1 | 1 | 0 |
| 0x08 | Sensorspannung | 1 | - | unsigned char | - | 18 | 255 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 17 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x943D | Übertemperatur FH-Fahrertuer |
| 0x943E | Übertemperatur FH-Beifahrertuer |
| 0x943F | LIN-Kommunikation defekt |
| 0x9440 | Einstiegsleuchte defekt |
| 0x9441 | CAN-Overrun |
| 0x9442 | Schaltnuss defekt |
| 0x9443 | Tuerkontakt defekt |
| 0x9444 | Schaltnuss Timeout |
| 0x9445 | MPM RES SVA |
| 0x9446 | MPM RES KLR |
| 0x9447 | MPM RES WECK |
| 0x9448 | MPM AUS CTR_CBR |
| 0x9449 | MPM AUS KLR |
| 0x944A | MPM AUS WECK |
| 0x944B | Unterspannung &lt;8V an Kl.30A oder 30B |
| 0x944C | Unterspannung &lt;7V an Kl.30A oder 30B |
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

Dimensions: 11 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9442 | 0x01 | 0x03 | - | - |
| 0x9444 | 0x01 | 0x03 | - | - |
| 0x9445 | 0x04 | 0x05 | - | - |
| 0x9446 | 0x04 | 0x05 | - | - |
| 0x9447 | 0x04 | 0x05 | - | - |
| 0x9448 | 0x04 | 0x05 | - | - |
| 0x9449 | 0x04 | 0x05 | - | - |
| 0x944A | 0x04 | 0x05 | - | - |
| 0x944B | 0x06 | 0x04 | - | - |
| 0x944C | 0x06 | 0x04 | - | - |
| default | 0x03 | 0x03 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x02 | Sensorspannung | Volt | - | unsigned char | - | 5 | 255 | 0 |
| 0x03 | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | Zeit 2 | sec | - | unsigned char | - | 65536 | 1 | 0 |
| 0x05 | Zeit 1 | sec | - | unsigned char | - | 524288 | 1 | 0 |
| 0x06 | Geschwindigkeit | km/h | - | unsigned char | - | 10 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-auswahl-spiegel"></a>
### AUSWAHL_SPIEGEL

Dimensions: 3 rows × 3 columns

| SPIEGEL | NAME | TEXT |
| --- | --- | --- |
| 0x01 | SPIEGEL_FA | Spiegel Fahrertuer auswaehlen |
| 0x02 | SPIEGEL_BF | Spiegel Beifahrertuer auswaehlen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-richtung-spiegel"></a>
### RICHTUNG_SPIEGEL

Dimensions: 7 rows × 3 columns

| SPIEGEL_R | NAME | TEXT |
| --- | --- | --- |
| 0x00 | NEUTRAL | Spiegel nicht bewegen |
| 0x01 | OBEN | Spiegel nach oben fahren |
| 0x02 | UNTEN | Spiegel nach unten fahren |
| 0x03 | LINKS | Spiegel nach links fahren |
| 0x04 | RECHTS | Spiegel nach rechts fahren |
| 0x05 | BEI/AUSKLAPPEN | Spiegel beiklappen/ausklappen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-spiegel-heizung"></a>
### SPIEGEL_HEIZUNG

Dimensions: 11 rows × 3 columns

| HEIZUNG | NAME | TEXT |
| --- | --- | --- |
| 0x00 | 0 | Spiegelheizung aus |
| 0x01 | 25 | Spiegelheizung 25% ein |
| 0x02 | 50 | Spiegelheizung 50% ein |
| 0x03 | 75 | Spiegelheizung 75% ein |
| 0x04 | 100 | Spiegelheizung 100% ein |
| 0x05 | 125 | Spiegelheizung 125% ein |
| 0x06 | UNBEGRENZT | Spiegelheizung unbegrenzt ein |
| 0x07 | UNGUELTIG | ungueltig |
| 0x08 | ECCOS_EIN | Spiegelheizung wird fuer ECCOS-Messung ausgeschalten |
| 0x09 | ECCOS_AUS | ECCOS-Messung beendet, Spiegelheizung wieder einschalten |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-steuern-servotronic"></a>
### STEUERN_SERVOTRONIC

Dimensions: 3 rows × 3 columns

| VORGABEART | NAME | TEXT |
| --- | --- | --- |
| 0x01 | STROM | Servowandler ueber Strom steuern |
| 0x02 | PWM | Servowandler ueber PWM steuern |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-auswahl-fenster"></a>
### AUSWAHL_FENSTER

Dimensions: 4 rows × 3 columns

| FH | NAME | TEXT |
| --- | --- | --- |
| 0x01 | FH_FA | Fensterheber Fahrertuer auswaehlen |
| 0x02 | FH_BF | Fensterheber Beifahrertuer auswaehlen |
| 0x03 | BEIDE_FH | beide Fensterheber auswaehlen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-steuern-mpm"></a>
### STEUERN_MPM

Dimensions: 4 rows × 3 columns

| MPM | NAME | TEXT |
| --- | --- | --- |
| 0x10 | MPM_EIN | MPM-Relais einschalten |
| 0x20 | MPM_AUS | MPM-Relais ausschalten |
| 0x30 | SV_AUS | Standverbraucher zeitkodiert ausschalten |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-steuern-licht"></a>
### STEUERN_LICHT

Dimensions: 9 rows × 3 columns

| LI_STE | NAME | TEXT |
| --- | --- | --- |
| 0x01 | ESL | Schaltet die Ausstiegsleuchte hart ein |
| 0x02 | ESL_DIM_EIN | Dimmt die Ausstiegsleuchte auf maximale Helligkeit |
| 0x03 | ESL_DIM_AUS | Dimmt die Ausstiegsleuchte ab |
| 0x04 | VFB | Schaltet die Vorfeldbeleuchtung hart ein |
| 0x05 | VFB_DIM_EIN | Dimmt die Vorfeldleuchte auf maximale Helligkeit |
| 0x06 | VFB_DIM_AUS | Dimmt die Vorfeldleuchte ab |
| 0x07 | LED1 | Schaltet die Beleuchtung der Funktionstaste 1 hart ein |
| 0x08 | LED2 | Schaltet die Beleuchtung der Funktionstaste 2 hart ein |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-steuern-zv"></a>
### STEUERN_ZV

Dimensions: 5 rows × 3 columns

| ZVZ | NAME | TEXT |
| --- | --- | --- |
| 0x01 | ER | beide Schlösser entriegeln |
| 0x02 | ES | beide Schlösser entsichern |
| 0x03 | VR | beide Schlösser verriegeln |
| 0x04 | ZS | beide Schlösser sichern |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-steuern-lara-pos"></a>
### STEUERN_LARA_POS

Dimensions: 7 rows × 6 columns

| NAME | DIR | MOD | EE | POS | REMARK |
| --- | --- | --- | --- | --- | --- |
| VERBAU1 | 0x01 | 2 | 1 | 0x000F | ca. 4mm (aus oberem Anschlag) |
| VERBAU2 | 0x01 | 2 | 1 | 0x0014 | ca. 6mm (aus oberem Anschlag) |
| VERBAU3 | 0x01 | 2 | 1 | 0x0019 | ca. 8mm (aus oberem Anschlag) |
| UNTEN | 0x01 | 2 | 1 | 0x0200 | unterer Anschlag |
| OBEN | 0x02 | 2 | 1 | 0x0000 | oberer Anschlag |
| DENORM | 0x00 | 2 | 0 | 0x0000 | denormiert das LCPA, keie Fahrt nach unten mehr moeglich |
| ERROR | 0x03 | 2 | 0 | 0 | ungültiges Argument |

<a id="table-steuern-fh-fat-bft"></a>
### STEUERN_FH_FAT_BFT

Dimensions: 13 rows × 3 columns

| ARGUMENT | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x01 | FH_FA_MAUT_AUF | Fensterheber Fahrerseite Maut oeffnen |
| 0x02 | FH_FA_AUF | Fensterheber Fahrerseite oeffnen |
| 0x03 | FH_FA_MAUT_ZU | Fensterheber Fahrerseite Maut schliessen |
| 0x04 | FH_FA_ZU | Fensterheber Fahrerseite schliessen |
| 0x05 | FH_BF_MAUT_AUF | Fensterheber Beifahrerseite Maut oeffnen |
| 0x06 | FH_BF_AUF | Fensterheber Beifahrerseite oeffnen |
| 0x07 | FH_BF_MAUT_ZU | Fensterheber Beifahrerseite Maut schliessen |
| 0x08 | FH_BF_ZU | Fensterheber Beifahrerseite schliessen |
| 0x11 | FH_FA_BF_MAUT_AUF | Fensterheber Fahrerseite und Beifahrerseite Maut oeffnen |
| 0x12 | FH_FA_BF_AUF | Fensterheber Fahrerseite Beifahrerseite oeffnen |
| 0x13 | FH_FA_BF_MAUT_ZU | Fensterheber Fahrerseite und Beifahrerseite Maut schliessen |
| 0x14 | FH_FA_BF_ZU | Fensterheber Fahrerseite Beifahrerseite schliessen |
| 0xXY | ERROR_ARGUMENT | fehlerhaftes Argument |

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
| 2 | FAHRERSEITE - REVERS_ISRDIAG |
| 3 | FAHRERSEITE - REVERS_BLOCK |
| 101 | BEIFAHRERSEITE - REVERS_ISR |
| 102 | BEIFAHRERSEITE - REVERS_ISRDIAG |
| 103 | BEIFAHRERSEITE - REVERS_BLOCK |
| 0xXY | undefiniert |

<a id="table-zuordnung-can-id-sg"></a>
### ZUORDNUNG_CAN_ID_SG

Dimensions: 409 rows × 6 columns

| CAN_ID_DEZ | CAN_ID_HEX | CAN_ID_NAME | DIAG_ID_DEZ | DIAG_ID_HEX | SG_NAME |
| --- | --- | --- | --- | --- | --- |
| 0 | 0x00 | unbekannt | 0 | 0x00 | Sender unbekannt |
| 949 | 0x3B5 | Status Wasserventil [6] | 120 | 0x78 | IHKA |
| 957 | 0x3BD | Status Verbraucherabschaltung [2] | 114 | 0x72 | KBM |
| 250 | 0xFA | Steuerung Fensterheber FAT [10] | 0 | 0x0 | KGM |
| 251 | 0xFB | Steuerung Fensterheber BFT [5] | 0 | 0x0 | KGM |
| 252 | 0xFC | Steuerung Fensterheber FATH [5] | 114 | 0x72 | KBM |
| 253 | 0xFD | Steuerung Fensterheber BFTH [5] | 114 | 0x72 | KBM |
| 168 | 0xA8 | Drehmoment 1 K-CAN [10] | 18 | 0x12 | DME1/DDE1 |
| 169 | 0xA9 | Drehmoment 2 (10) | 18 | 0x12 | DME1/DDE1 |
| 170 | 0xAA | Drehmoment 3 K-CAN [10] | 18 | 0x12 | DME1/DDE1 |
| 172 | 0xAC | Radmoment Antriebsstrang 2 [5] | 18 | 0x12 | DME1/DDE1 |
| 173 | 0xAD | Verzögerungsanforderung ACC [9] | 28 | 0x1C | LDM |
| 173 | 0xAD | Verzögerungsanforderung ACC [9] | 33 | 0x21 | ACC_Modul/ACC+NAVI |
| 179 | 0xB3 | Steuerung Lenkunterstützung [2] | 22 | 0x16 | AFS |
| 180 | 0xB4 | Radmoment Antriebsstrang 1 [4] | 18 | 0x12 | DME1/DDE1 |
| 181 | 0xB5 | Drehmomentanforderung EGS [9] | 24 | 0x18 | EGS_MECH+NAVI/EGS_MECH |
| 182 | 0xB6 | Drehmomentanforderung DSC [7] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 183 | 0xB7 | Drehmomentanforderung ACC [10] | 28 | 0x1C | LDM |
| 183 | 0xB7 | Drehmomentanforderung ACC [10] | 33 | 0x21 | ACC_Modul/ACC+NAVI |
| 184 | 0xB8 | Drehmomentanforderung DKG [2] | 24 | 0x18 | DKG |
| 185 | 0xB9 | Drehmomentanforderung AFS [3] | 22 | 0x16 | AFS |
| 186 | 0xBA | Getriebedaten [20] | 24 | 0x18 | SMG_M/SMG/EGS_MECH+NAVI/EGS_MECH/DKG |
| 187 | 0xBB | Sollmomentanforderung [7] | 41 | 0x29 | DXC_RB |
| 188 | 0xBC | Status Sollmomentumsetzung [7] | 25 | 0x19 | VGSG |
| 189 | 0xBD | Drehmomentanforderung SSG [6] | 24 | 0x18 | SMG_M/SMG |
| 190 | 0xBE | Alive Zähler [12] | 35 | 0x23 | ARS_Modul |
| 191 | 0xBF | Anforderung Radmoment Antriebsstrang [6] | 28 | 0x1C | LDM |
| 192 | 0xC0 | Alive Zentrales Gateway [1] | 0 | 0x0 | KGM |
| 193 | 0xC1 | Alive Zähler Telefon [3] | 54 | 0x36 | TEL_JAP/TEL_BPI |
| 196 | 0xC4 | Lenkradwinkel K-CAN [13] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 200 | 0xC8 | Lenkradwinkel Oben K-CAN [6] | 2 | 0x2 | SZL_LWS |
| 206 | 0xCE | Radgeschwindigkeit K-CAN [4] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 210 | 0xD2 | Bedienung Sitzverstellung BF [6] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 213 | 0xD5 | Anforderung Radmoment Bremse [6] | 28 | 0x1C | LDM |
| 215 | 0xD7 | Alive Zähler Sicherheit [2] | 1 | 0x1 | ACSM |
| 218 | 0xDA | Bedienung Sitzverstellung FA [6] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 225 | 0xE1 | Radmoment Bremse [3] | 41 | 0x29 | DXC_RB/DSC_RB |
| 226 | 0xE2 | Status Zentralverriegelung BFT [11] | 0 | 0x0 | KGM |
| 230 | 0xE6 | Status Zentralverriegelung BFTH [11] | 114 | 0x72 | KBM |
| 234 | 0xEA | Status Zentralverriegelung FAT [11] | 0 | 0x0 | KGM |
| 238 | 0xEE | Status Zentralverriegelung FATH [11] | 114 | 0x72 | KBM |
| 242 | 0xF2 | Status Zentralverriegelung HK [13] | 114 | 0x72 | KBM |
| 246 | 0xF6 | Steuerung Außenspiegel [9] | 0 | 0x0 | KGM |
| 304 | 0x130 | Klemmenstatus [19] | 64 | 0x40 | CAS |
| 309 | 0x135 | Steuerung Crashabschaltung EKP [1] | 1 | 0x1 | ACSM |
| 351 | 0x15F | Anforderung Winkel FFP [6] | 28 | 0x1C | LDM |
| 370 | 0x172 | Quittierung Anforderung Kombi [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 400 | 0x190 | Anzeige ACC [13] | 28 | 0x1C | LDM |
| 400 | 0x190 | Anzeige ACC [13] | 33 | 0x21 | ACC_Modul/ACC+NAVI |
| 402 | 0x192 | Bedienung Getriebewahlschalter [16] | 2 | 0x2 | SZL_LWS |
| 403 | 0x193 | Anzeige ACC DCC [4] | 28 | 0x1C | LDM |
| 404 | 0x194 | Bedienung Tempomat/ACC [13] | 2 | 0x2 | SZL_LWS |
| 408 | 0x198 | Bedienung Getriebewahlschalter 2 [2] | 94 | 0x5E | GWS |
| 414 | 0x19E | Status DSC K-CAN [19] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 416 | 0x1A0 | Geschwindigkeit K-CAN [14] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 418 | 0x1A2 | Getriebedaten 2 [6] | 24 | 0x18 | EGS_MECH+NAVI/EGS_MECH/DKG |
| 419 | 0x1A3 | Rohdaten Längsbeschleunigung [3] | 24 | 0x18 | SMG_M |
| 422 | 0x1A6 | Wegstrecke [6] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 426 | 0x1AA | Effekt ErgoCommander [10] | 98 | 0x62 | M_ASK/CCC_GW |
| 428 | 0x1AC | Status ARS-Modul [13] | 35 | 0x23 | ARS_Modul |
| 436 | 0x1B4 | Status Kombi [14] | 96 | 0x60 | Kombi |
| 437 | 0x1B5 | Wärmestrom/Lastmoment Klima [14] | 120 | 0x78 | IHKA |
| 438 | 0x1B6 | Wärmestrom Motor [11] | 18 | 0x12 | DME1/DDE1 |
| 440 | 0x1B8 | Bedienung ErgoCommander [6] | 103 | 0x67 | ZBE_LO/ZBE |
| 450 | 0x1C2 | Abstandsmeldung PDC [5] | 100 | 0x64 | PDC |
| 451 | 0x1C3 | Abstandsmeldung 2 PDC [3] | 100 | 0x64 | PDC |
| 454 | 0x1C6 | Akustikmeldung PDC [5] | 100 | 0x64 | PDC |
| 464 | 0x1D0 | Motordaten [13] | 18 | 0x12 | DME1/DDE1 |
| 466 | 0x1D2 | Anzeige Getriebedaten [22] | 24 | 0x18 | SMG_M/SMG/EGS_MECH+NAVI/EGS_MECH/DKG |
| 470 | 0x1D6 | Bedienung Taster Audio/Telefon [12] | 2 | 0x2 | SZL_LWS |
| 472 | 0x1D8 | Bedienung Klima Luftverteilung FA [13] | 98 | 0x62 | M_ASK/CCC_GW |
| 473 | 0x1D9 | Bedienung Taster M-Drive [2] | 2 | 0x2 | SZL_LWS |
| 474 | 0x1DA | Bedienung Klima Fernwirken [5] | 64 | 0x40 | CAS |
| 476 | 0x1DC | Bedienung Schichtung Sitzheizung [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 480 | 0x1E0 | Bedienung Klima Luftverteilung BF [7] | 98 | 0x62 | M_ASK/CCC_GW |
| 482 | 0x1E2 | Bedienung Klima Front [11] | 98 | 0x62 | M_ASK/CCC_GW |
| 487 | 0x1E7 | Bedienung Sitzheizung/Sitzklima FA [7] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 488 | 0x1E8 | Bedienung Sitzheizung/Sitzklima BF [7] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 490 | 0x1EA | Bedienung Lenksäulenverstellung [5] | 2 | 0x2 | SZL_LWS |
| 491 | 0x1EB | Bedienung Aktivsitz FA [3] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 492 | 0x1EC | Bedienung Aktivsitz BF [3] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 493 | 0x1ED | Bedienung Lehnenbreitenverstellung Aktiv FA [2] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 494 | 0x1EE | Bedienung Lenkstockstaster [6] | 2 | 0x2 | SZL_LWS |
| 495 | 0x1EF | Bedienung Lehnenbreitenverstellung Aktiv BF [2] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 498 | 0x1F2 | Bedienung Sitzmemory BF [3] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 499 | 0x1F3 | Bedienung Sitzmemory FA [4] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 500 | 0x1F4 | Fernbedienung Sitzmemory BF [2] | 255 | 0xFF | unbekannt |
| 502 | 0x1F6 | Blinken [6] | 112 | 0x70 | LM |
| 508 | 0x1FC | Status AFS [4] | 22 | 0x16 | AFS |
| 510 | 0x1FE | Crash [12] | 1 | 0x1 | ACSM |
| 512 | 0x200 | Regelgeschwindigkeit Stufentempomat [7] | 18 | 0x12 | DME1/DDE1 |
| 514 | 0x202 | Dimmung [10] | 112 | 0x70 | LM |
| 517 | 0x205 | Akustikanforderung Kombi [3] | 96 | 0x60 | Kombi |
| 518 | 0x206 | Steuerung Anzeige Shiftlights [1] | 18 | 0x12 | DME1 |
| 523 | 0x20B | Memoryverstellung [6] | 101 | 0x65 | SZM_MIT_KBUS |
| 523 | 0x20B | Memoryverstellung [6] | 109 | 0x6D | SM_FA |
| 524 | 0x20C | Steuerung Lenksäule (4) | 109 | 0x6D | SM_FA |
| 525 | 0x20D | Position Lenksäule (5) | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 528 | 0x210 | Bedienung HUD [7] | 98 | 0x62 | M_ASK/CCC_GW |
| 529 | 0x211 | Status HUD [7] | 61 | 0x3D | HUD |
| 530 | 0x212 | Höhenstände Luftfeder [8] | 56 | 0x38 | EHC |
| 538 | 0x21A | Lampenzustand [13] | 112 | 0x70 | LM |
| 540 | 0x21C | Bedienung Night-Vision [2] | 98 | 0x62 | CCC_GW |
| 542 | 0x21E | Status Night-Vision [2] | 87 | 0x57 | NVC |
| 550 | 0x226 | Regensensor-Wischergeschwindigkeit [8] | 69 | 0x45 | RLS |
| 550 | 0x226 | Regensensor-Wischergeschwindigkeit [8] | 112 | 0x70 | LM |
| 552 | 0x228 | Bedienung Sonderfunktion [8] | 98 | 0x62 | M_ASK/CCC_GW |
| 552 | 0x228 | Bedienung Sonderfunktion [8] | 99 | 0x63 | CCC_MM |
| 554 | 0x22A | Status BFS [10] | 110 | 0x6E | SM_BF |
| 558 | 0x22E | Status BFSH [7] | 255 | 0xFF | unbekannt |
| 562 | 0x232 | Status FAS [10] | 109 | 0x6D | SM_FA |
| 566 | 0x236 | Status FASH [7] | 255 | 0xFF | unbekannt |
| 567 | 0x237 | Status Lehnenbreitenverstellung Aktiv BF [3] | 90 | 0x5A | aLBV_BF |
| 569 | 0x239 | Status Lehnenbreitenverstellung Aktiv FA [3] | 89 | 0x59 | aLBV_FA |
| 570 | 0x23A | Status Funkschlüssel [13] | 64 | 0x40 | CAS |
| 571 | 0x23B | Status Klima Front Erweitert [1] | 120 | 0x78 | IHKA |
| 572 | 0x23C | Status Bedienung Sitzkomfort FA [1] | 109 | 0x6D | SM_FA |
| 575 | 0x23F | Status Bedienung Sitzkomfort BF [1] | 110 | 0x6E | SM_BF |
| 578 | 0x242 | Status Klima Front [11] | 120 | 0x78 | IHKA |
| 586 | 0x24A | Status PDC [6] | 100 | 0x64 | PDC |
| 594 | 0x252 | Wischerstatus [8] | 114 | 0x72 | KBM |
| 598 | 0x256 | Challenge Passive Access [10] | 64 | 0x40 | CAS |
| 600 | 0x258 | Status Transmission Passive Access [4] | 39 | 0x27 | PGS |
| 604 | 0x25C | Bedienung Klima Zusatzprogramme [2] | 98 | 0x62 | M_ASK/CCC_GW |
| 619 | 0x26B | Bedienung Rollos BF [2] | 255 | 0xFF | unbekannt |
| 620 | 0x26C | Bedienung Rollos FA [2] | 0 | 0x0 | KGM |
| 621 | 0x26D | Bedienung Rollos MK [1] | 255 | 0xFF | unbekannt |
| 622 | 0x26E | Steuerung FH/SHD Zentrale (Komfort) [10] | 64 | 0x40 | CAS |
| 623 | 0x26F | Bedienung Rollos BFH [2] | 255 | 0xFF | unbekannt |
| 624 | 0x270 | Bedienung Rollos FAH [2] | 255 | 0xFF | unbekannt |
| 632 | 0x278 | Navigationsgraph [3] | 98 | 0x62 | CCC_GW |
| 634 | 0x27A | Synchronisation Navigationsgraph [4] | 98 | 0x62 | CCC_GW |
| 638 | 0x27E | Status Verdeck Cabrio [7] | 36 | 0x24 | CVM_V |
| 644 | 0x284 | Steuerung Fernstart Sicherheitsfahrzeug [8] | 64 | 0x40 | CAS |
| 645 | 0x285 | Steuerung Rollos [3] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 652 | 0x28C | Bedienung Taster Vertikaldynamik [2] | 94 | 0x5E | GWS |
| 656 | 0x290 | Steuerung Reaktion Wasserstoff-Fahrzeug [1] | 255 | 0xFF | unbekannt |
| 658 | 0x292 | Steuerung Fernlicht-Assistent [2] | 95 | 0x5F | FLA |
| 671 | 0x29F | Fernbedienung FondCommander [5] | 64 | 0x40 | CAS |
| 672 | 0x2A0 | Steuerung Zentralverriegelung [10] | 64 | 0x40 | CAS |
| 674 | 0x2A2 | Bedienung Klima Standfunktionen [5] | 98 | 0x62 | M_ASK/CCC_GW |
| 676 | 0x2A4 | Bedienung Personalisierung [8] | 98 | 0x62 | M_ASK/CCC_GW |
| 678 | 0x2A6 | Bedienung Wischertaster [12] | 2 | 0x2 | SZL_LWS |
| 690 | 0x2B2 | Raddrücke K-CAN [1] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 691 | 0x2B3 | Beschleunigungsdaten [2] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 692 | 0x2B4 | DWA-Alarm [4] | 65 | 0x41 | DWA |
| 694 | 0x2B6 | Steuerung Hupe DWA [3] | 65 | 0x41 | DWA |
| 696 | 0x2B8 | Bedienung Bordcomputer [3] | 98 | 0x62 | M_ASK/CCC_GW |
| 698 | 0x2BA | Stoppuhr (3) | 96 | 0x60 | Kombi |
| 704 | 0x2C0 | LCD-Leuchtdichte [7] | 96 | 0x60 | Kombi |
| 714 | 0x2CA | Außentemperatur [9] | 96 | 0x60 | Kombi |
| 718 | 0x2CE | Steuerung Monitor [4] | 98 | 0x62 | M_ASK/CCC_GW |
| 725 | 0x2D5 | Status Heizung Heckscheibe [1] | 120 | 0x78 | IHKA |
| 730 | 0x2DA | Status Heckklappenlift [2] | 107 | 0x6B | HKL |
| 738 | 0x2E2 | Status Einstellung Video Night-Vision [1] | 87 | 0x57 | NVC |
| 740 | 0x2E4 | Status Anhänger (8) | 113 | 0x71 | AHM |
| 742 | 0x2E6 | Status Klima Luftverteilung FA [13] | 120 | 0x78 | IHKA |
| 746 | 0x2EA | Status Klima Luftverteilung BF [9] | 120 | 0x78 | IHKA |
| 748 | 0x2EC | Status Klima SH/ZH Zusatzwasserpumpe [14] | 122 | 0x7A | SH_ZH |
| 750 | 0x2EE | Status Klima Zusatzprogramme [2] | 120 | 0x78 | IHKA |
| 752 | 0x2F0 | Status Klima Standfunktionen [12] | 120 | 0x78 | IHKA |
| 756 | 0x2F4 | Steuerung Klima SH/ZH Zusatzwasserpumpe [13] | 120 | 0x78 | IHKA |
| 758 | 0x2F6 | Steuerung Licht [7] | 114 | 0x72 | KBM |
| 759 | 0x2F7 | Einheiten [10] | 98 | 0x62 | M_ASK/CCC_GW |
| 759 | 0x2F7 | Einheiten [10] | 99 | 0x63 | CCC_MM |
| 760 | 0x2F8 | Uhrzeit/Datum [12] | 96 | 0x60 | Kombi |
| 762 | 0x2FA | Sitzbelegung Gurtkontakte (14) | 1 | 0x1 | ACSM |
| 764 | 0x2FC | ZV und Klappenzustand [11] | 64 | 0x40 | CAS |
| 772 | 0x304 | Status Gang [13] | 24 | 0x18 | SMG_M/SMG/EGS_MECH+NAVI/EGS_MECH/DKG |
| 774 | 0x306 | Fahrzeugneigung [2] | 112 | 0x70 | LM |
| 776 | 0x308 | Status MSA [2] | 18 | 0x12 | DME1/DDE1 |
| 784 | 0x310 | Außentemperatur/Relativzeit [10] | 96 | 0x60 | Kombi |
| 785 | 0x311 | Nachtankmenge [3] | 96 | 0x60 | Kombi |
| 786 | 0x312 | Service Call Teleservice [2] | 96 | 0x60 | Kombi |
| 787 | 0x313 | Status Service Call Teleservice [3] | 54 | 0x36 | TEL_BPI |
| 787 | 0x313 | Status Service Call Teleservice [3] | 98 | 0x62 | M_ASK/CCC_GW |
| 788 | 0x314 | Status Fahrlicht [9] | 69 | 0x45 | RLS |
| 788 | 0x314 | Status Fahrlicht [9] | 112 | 0x70 | LM |
| 789 | 0x315 | Fahrzeugmodus [7] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 791 | 0x317 | Bedienung Taster PDC [1] | 101 | 0x65 | SZM_MIT_KBUS/SZM |
| 792 | 0x318 | Status Antennen Passive Access [7] | 39 | 0x27 | PGS |
| 793 | 0x319 | Bedienung Taster RDC [4] | 101 | 0x65 | SZM |
| 796 | 0x31C | Status Reifendruck [6] | 32 | 0x20 | RDC |
| 797 | 0x31D | Status Reifenpannenanzeige [6] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 802 | 0x322 | Dämpferstrom [2] | 57 | 0x39 | EDCK_Modul |
| 806 | 0x326 | Status Dämpferprogramm [9] | 57 | 0x39 | EDCK_Modul |
| 808 | 0x328 | Relativzeit [9] | 96 | 0x60 | Kombi |
| 810 | 0x32A | Steuerung ALC [2] | 112 | 0x70 | LM |
| 813 | 0x32D | Anzeige HDC [3] | 41 | 0x29 | DXC_RB |
| 814 | 0x32E | Status Klima Interne Regelinfo [6] | 120 | 0x78 | IHKA |
| 816 | 0x330 | Kilometerstand/Reichweite [5] | 96 | 0x60 | Kombi |
| 817 | 0x331 | Programmierung Stufentempomat [2] | 98 | 0x62 | M_ASK/CCC_GW |
| 818 | 0x332 | Fahreranzeige Drehzahlbereich [4] | 18 | 0x12 | DME1/DDE1 |
| 821 | 0x335 | Status Elektrische Kraftstoffpumpe [3] | 23 | 0x17 | EKP |
| 822 | 0x336 | Anzeige Checkcontrol-Meldung (Rolle) [3] | 96 | 0x60 | Kombi |
| 823 | 0x337 | Status Kraftstoffregelung DME [1] | 18 | 0x12 | DME1 |
| 824 | 0x338 | Steuerung Anzeige Checkcontrol-Meldung [7] | 96 | 0x60 | Kombi |
| 825 | 0x339 | Status Anzeige Funktionen Extern [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 826 | 0x33A | Status Monitor Front [3] | 115 | 0x73 | CID_C_H/CID_C |
| 840 | 0x348 | Übereinstimmung Navigationsgraph [4] | 98 | 0x62 | CCC_GW |
| 842 | 0x34A | Navigation GPS 1 [5] | 98 | 0x62 | CCC_GW |
| 843 | 0x34B | Status Sitzlehnenverriegelung FA (3) | 101 | 0x65 | SZM_MIT_KBUS |
| 843 | 0x34B | Status Sitzlehnenverriegelung FA (3) | 109 | 0x6D | SM_FA |
| 844 | 0x34C | Navigation GPS 2 [5] | 98 | 0x62 | CCC_GW |
| 845 | 0x34D | Status Sitzlehnenverriegelung BF [2] | 101 | 0x65 | SZM_MIT_KBUS |
| 845 | 0x34D | Status Sitzlehnenverriegelung BF [2] | 110 | 0x6E | SM_BF |
| 846 | 0x34E | Navigation System Information [6] | 98 | 0x62 | CCC_GW |
| 858 | 0x35A | Termin Condition Based Service [2] | 98 | 0x62 | M_ASK/CCC_GW |
| 860 | 0x35C | Status Bordcomputer [5] | 96 | 0x60 | Kombi |
| 862 | 0x35E | Daten Bordcomputer (Reisedaten) [5] | 96 | 0x60 | Kombi |
| 864 | 0x360 | Daten Bordcomputer (Fahrtbeginn) [2] | 96 | 0x60 | Kombi |
| 866 | 0x362 | Daten Bordcomputer (Durchschnittswerte) [4] | 96 | 0x60 | Kombi |
| 868 | 0x364 | Daten Bordcomputer (Ankunft) [2] | 96 | 0x60 | Kombi |
| 870 | 0x366 | Anzeige Kombi/Externe Anzeige [3] | 96 | 0x60 | Kombi |
| 871 | 0x367 | Steuerung Anzeige Bedarfsorientierter Service [6] | 96 | 0x60 | Kombi |
| 884 | 0x374 | Radtoleranzabgleich [7] | 41 | 0x29 | DXC_RB/DSC_RB/DSC_CT |
| 886 | 0x376 | Status Verschleiß Lamelle [3] | 25 | 0x19 | VGSG |
| 896 | 0x380 | Fahrgestellnummer [5] | 64 | 0x40 | CAS |
| 897 | 0x381 | Elektronischer Motorölmessstab [10] | 18 | 0x12 | DME1/DDE1 |
| 898 | 0x382 | Elektronischer Motorölmessstab M [1] | 18 | 0x12 | DME1/DDE1 |
| 904 | 0x388 | Fahrzeugtyp [13] | 64 | 0x40 | CAS |
| 910 | 0x38E | Startdrehzahl [1] | 18 | 0x12 | DME1/DDE1 |
| 916 | 0x394 | RDA Anfrage/Datenablage [5] | 96 | 0x60 | Kombi |
| 917 | 0x395 | Codierung Powermanagement [2] | 64 | 0x40 | CAS |
| 920 | 0x398 | Bedienung Fahrwerk [14] | 98 | 0x62 | M_ASK/CCC_GW |
| 921 | 0x399 | Status M-Drive [2] | 18 | 0x12 | DME1 |
| 924 | 0x39C | EBA Datenanforderung [5] | 255 | 0xFF | unbekannt |
| 926 | 0x39E | Bedienung Uhrzeit/Datum [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 928 | 0x3A0 | Fahrzeugzustand [4] | 0 | 0x0 | KGM |
| 931 | 0x3A3 | Anforderung Remote Services [2] | 98 | 0x62 | M_ASK/CCC_GW |
| 940 | 0x3AC | Nachlaufzeit Klemme 30 fehlergesteuert [2] | 0 | 0x0 | KGM |
| 944 | 0x3B0 | Status Gang Rückwärts [2] | 112 | 0x70 | LM |
| 945 | 0x3B1 | Getriebedaten 3 [2] | 24 | 0x18 | EGS_MECH/DKG |
| 947 | 0x3B3 | Powermanagement Verbrauchersteuerung [8] | 18 | 0x12 | DME1/DDE1 |
| 948 | 0x3B4 | Powermanagement Batteriespannung [11] | 18 | 0x12 | DME1/DDE1 |
| 950 | 0x3B6 | Position Fensterheber FAT [6] | 0 | 0x0 | KGM |
| 951 | 0x3B7 | Position Fensterheber FATH [5] | 114 | 0x72 | KBM |
| 952 | 0x3B8 | Position Fensterheber BFT [6] | 0 | 0x0 | KGM |
| 953 | 0x3B9 | Position Fensterheber BFTH [5] | 114 | 0x72 | KBM |
| 954 | 0x3BA | Position SHD [10] | 68 | 0x44 | SHD/MDS |
| 958 | 0x3BE | Nachlaufzeit Stromversorgung [5] | 64 | 0x40 | CAS |
| 959 | 0x3BF | Position Fensterheber Heckscheibe [1] | 36 | 0x24 | CVM_V |
| 960 | 0x3C0 | Konfiguration FAS [3] | 109 | 0x6D | SM_FA |
| 961 | 0x3C1 | Konfiguration BFS [3] | 110 | 0x6E | SM_BF |
| 970 | 0x3CA | Konfiguration M-Drive [2] | 98 | 0x62 | M_ASK/CCC_GW |
| 979 | 0x3D3 | Status Solarsensor [1] | 112 | 0x70 | LM |
| 980 | 0x3D4 | Konfiguration Zentralverriegelung CKM [3] | 98 | 0x62 | M_ASK/CCC_GW |
| 981 | 0x3D5 | Status Zentralverriegelung CKM [4] | 64 | 0x40 | CAS |
| 982 | 0x3D6 | Konfiguration DWA CKM [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 983 | 0x3D7 | Status DWA CKM [2] | 65 | 0x41 | DWA |
| 984 | 0x3D8 | Konfiguration RLS CKM [3] | 98 | 0x62 | M_ASK/CCC_GW |
| 985 | 0x3D9 | Status RLS CKM [4] | 69 | 0x45 | RLS |
| 985 | 0x3D9 | Status RLS CKM [4] | 112 | 0x70 | LM |
| 986 | 0x3DA | Konfiguration Memorypositionen CKM [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 987 | 0x3DB | Status Memorypositionen CKM [3] | 101 | 0x65 | SZM_MIT_KBUS |
| 987 | 0x3DB | Status Memorypositionen CKM [3] | 109 | 0x6D | SM_FA |
| 988 | 0x3DC | Konfiguration Licht CKM [3] | 98 | 0x62 | M_ASK/CCC_GW |
| 989 | 0x3DD | Status Licht CKM [4] | 112 | 0x70 | LM |
| 990 | 0x3DE | Konfiguration Klima CKM [5] | 98 | 0x62 | M_ASK/CCC_GW |
| 991 | 0x3DF | Status Klima CKM [6] | 120 | 0x78 | IHKA |
| 992 | 0x3E0 | Konfiguration ALC CKM [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 993 | 0x3E1 | Status ALC CKM [1] | 112 | 0x70 | LM |
| 994 | 0x3E2 | Konfiguration Heckklappe CKM [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 995 | 0x3E3 | Status Heckklappe CKM [1] | 107 | 0x6B | HKL |
| 1001 | 0x3E9 | Marker 1 [1] | 255 | 0xFF | unbekannt |
| 1002 | 0x3EA | Marker 2 [3] | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 1003 | 0x3EB | Marker 3 [1] | 125 | 0x7D | Diagnosetool_PT_CAN |
| 1006 | 0x3EE | Anforderung Fehlermeldung [1] | 255 | 0xFF | unbekannt |
| 1007 | 0x3EF | OBD Daten Motor (3) | 18 | 0x12 | DME1/DDE1 |
| 1008 | 0x3F0 | Konfiguration Licht Erweitert CKM [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 1009 | 0x3F1 | Status Licht Erweitert CKM [1] | 112 | 0x70 | LM |
| 1012 | 0x3F4 | Konfiguration Laderaumabdeckung CKM [1] | 98 | 0x62 | M_ASK/CCC_GW |
| 1013 | 0x3F5 | Status Laderaumabdeckung CKM [1] | 114 | 0x72 | KBM |
| 1022 | 0x3FE | Anforderung CAN_Testtool SI-Bus [5] | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 1280 | 0x500 | Datentransfer [1] | 112 | 0x70 | LM |
| 1280 | 0x500 | Datentransfer [1] | 120 | 0x78 | IHKA |
| 1984 | 0x7C0 | CAS Programmierung Bandende 1 (3) | 64 | 0x40 | CAS |
| 1985 | 0x7C1 | CAS Programmierung Bandende 2 (3) | 255 | 0xFF | TOOL_BANDENDE_CAS |
| 1986 | 0x7C2 | CAS Applikationsnachricht 1 (3) | 64 | 0x40 | CAS |
| 1987 | 0x7C3 | CAS Applikationsnachricht 2 (3) | 255 | 0xFF | TOOL_BANDENDE_CAS |
| 1152 | 0x480 | Netzwerkmanagement | 0 | 0x0 | KGM |
| 1153 | 0x481 | Netzwerkmanagement | 1 | 0x1 | ACSM |
| 1154 | 0x482 | Netzwerkmanagement | 2 | 0x2 | SZL_LWS |
| 1170 | 0x492 | Netzwerkmanagement | 18 | 0x12 | DDE1/DME1 |
| 1174 | 0x496 | Netzwerkmanagement | 22 | 0x16 | AFS |
| 1175 | 0x497 | Netzwerkmanagement | 23 | 0x17 | EKP |
| 1176 | 0x498 | Netzwerkmanagement | 24 | 0x18 | DKG/EGS_MECH/EGS_MECH+NAVI/SMG/SMG_M |
| 1177 | 0x499 | Netzwerkmanagement | 25 | 0x19 | VGSG |
| 1179 | 0x49B | Netzwerkmanagement | 27 | 0x1B | VVT1 |
| 1180 | 0x49C | Netzwerkmanagement | 28 | 0x1C | LDM |
| 1182 | 0x49E | Netzwerkmanagement | 30 | 0x1E | VVT2 |
| 1184 | 0x4A0 | Netzwerkmanagement | 32 | 0x20 | RDC |
| 1185 | 0x4A1 | Netzwerkmanagement | 33 | 0x21 | ACC+NAVI/ACC_Modul |
| 1187 | 0x4A3 | Netzwerkmanagement | 35 | 0x23 | ARS_Modul |
| 1188 | 0x4A4 | Netzwerkmanagement | 36 | 0x24 | CVM_V |
| 1189 | 0x4A5 | Netzwerkmanagement | 37 | 0x25 | RSC_VDA/SC_CT/SC_VDA |
| 1191 | 0x4A7 | Netzwerkmanagement | 39 | 0x27 | PGS |
| 1193 | 0x4A9 | Netzwerkmanagement | 41 | 0x29 | DSC_CT/DSC_RB/DXC_RB |
| 1206 | 0x4B6 | Netzwerkmanagement | 54 | 0x36 | TEL_BPI/TEL_JAP/TEL_MULF |
| 1207 | 0x4B7 | Netzwerkmanagement | 55 | 0x37 | AMP_TOP |
| 1208 | 0x4B8 | Netzwerkmanagement | 56 | 0x38 | EHC |
| 1209 | 0x4B9 | Netzwerkmanagement | 57 | 0x39 | EDCK_Modul |
| 1210 | 0x4BA | Netzwerkmanagement | 58 | 0x3A | KHM |
| 1211 | 0x4BB | Netzwerkmanagement | 59 | 0x3B | JNAV |
| 1212 | 0x4BC | Netzwerkmanagement | 60 | 0x3C | CDC |
| 1213 | 0x4BD | Netzwerkmanagement | 61 | 0x3D | HUD |
| 1216 | 0x4C0 | Netzwerkmanagement | 64 | 0x40 | CAS |
| 1217 | 0x4C1 | Netzwerkmanagement | 65 | 0x41 | DWA |
| 1220 | 0x4C4 | Netzwerkmanagement | 68 | 0x44 | MDS/SHD |
| 1221 | 0x4C5 | Netzwerkmanagement | 69 | 0x45 | RLS/RLS |
| 1227 | 0x4CB | Netzwerkmanagement | 75 | 0x4B | VM |
| 1232 | 0x4D0 | Netzwerkmanagement | 80 | 0x50 | Notstrom-Sirene |
| 1235 | 0x4D3 | Netzwerkmanagement | 83 | 0x53 | IBOC |
| 1236 | 0x4D4 | Netzwerkmanagement | 84 | 0x54 | SDARS |
| 1237 | 0x4D5 | Netzwerkmanagement | 85 | 0x55 | ISpeechBox |
| 1239 | 0x4D7 | Netzwerkmanagement | 87 | 0x57 | NVC |
| 1241 | 0x4D9 | Netzwerkmanagement | 89 | 0x59 | aLBV_FA |
| 1242 | 0x4DA | Netzwerkmanagement | 90 | 0x5A | aLBV_BF |
| 1243 | 0x4DB | Netzwerkmanagement | 91 | 0x5B | DAB |
| 1244 | 0x4DC | Netzwerkmanagement | 92 | 0x5C | Behoerde |
| 1245 | 0x4DD | Netzwerkmanagement | 93 | 0x5D | TLC |
| 1246 | 0x4DE | Netzwerkmanagement | 94 | 0x5E | GWS |
| 1247 | 0x4DF | Netzwerkmanagement | 95 | 0x5F | FLA |
| 1248 | 0x4E0 | Netzwerkmanagement | 96 | 0x60 | Kombi |
| 1250 | 0x4E2 | Netzwerkmanagement | 98 | 0x62 | CCC_GW/M_ASK |
| 1251 | 0x4E3 | Netzwerkmanagement | 99 | 0x63 | CCC_MM |
| 1252 | 0x4E4 | Netzwerkmanagement | 100 | 0x64 | PDC |
| 1253 | 0x4E5 | Netzwerkmanagement | 101 | 0x65 | SZM/SZM_MIT_KBUS |
| 1255 | 0x4E7 | Netzwerkmanagement | 103 | 0x67 | ZBE/ZBE_LO |
| 1259 | 0x4EB | Netzwerkmanagement | 107 | 0x6B | HKL |
| 1261 | 0x4ED | Netzwerkmanagement | 109 | 0x6D | SM_FA/SM_FA_KBUS |
| 1262 | 0x4EE | Netzwerkmanagement | 110 | 0x6E | SM_BF/SM_BF_KBUS |
| 1264 | 0x4F0 | Netzwerkmanagement | 112 | 0x70 | LM/LM_ALC |
| 1265 | 0x4F1 | Netzwerkmanagement | 113 | 0x71 | AHM |
| 1266 | 0x4F2 | Netzwerkmanagement | 114 | 0x72 | KBM |
| 1267 | 0x4F3 | Netzwerkmanagement | 115 | 0x73 | CID_C/CID_C_H |
| 1272 | 0x4F8 | Netzwerkmanagement | 120 | 0x78 | IHKA |
| 1274 | 0x4FA | Netzwerkmanagement | 122 | 0x7A | SH_ZH |
| 1277 | 0x4FD | Netzwerkmanagement | 125 | 0x7D | Diagnosetool_PT_CAN |
| 1278 | 0x4FE | Netzwerkmanagement | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 1289 | 0x509 | Netzwerkmanagement | 137 | 0x89 | Xenon_Scheinwerfer_Links_ALC |
| 1290 | 0x50A | Netzwerkmanagement | 138 | 0x8A | Xenon_Scheinwerfer_Rechts_ALC |
| 1291 | 0x50B | Netzwerkmanagement | 139 | 0x8B | CNV |
| 1393 | 0x571 | Netzwerkmanagement | 241 | 0xF1 | Diagnosedose |
| 1408 | 0x580 | Dienste | 0 | 0x0 | KGM |
| 1409 | 0x581 | Dienste | 1 | 0x1 | ACSM |
| 1410 | 0x582 | Dienste | 2 | 0x2 | SZL_LWS |
| 1426 | 0x592 | Dienste | 18 | 0x12 | DDE1/DME1 |
| 1430 | 0x596 | Dienste | 22 | 0x16 | AFS |
| 1431 | 0x597 | Dienste | 23 | 0x17 | EKP |
| 1432 | 0x598 | Dienste | 24 | 0x18 | DKG/EGS_MECH/EGS_MECH+NAVI/SMG/SMG_M |
| 1433 | 0x599 | Dienste | 25 | 0x19 | VGSG |
| 1435 | 0x59B | Dienste | 27 | 0x1B | VVT1 |
| 1436 | 0x59C | Dienste | 28 | 0x1C | LDM |
| 1438 | 0x59E | Dienste | 30 | 0x1E | VVT2 |
| 1440 | 0x5A0 | Dienste | 32 | 0x20 | RDC |
| 1441 | 0x5A1 | Dienste | 33 | 0x21 | ACC+NAVI/ACC_Modul |
| 1443 | 0x5A3 | Dienste | 35 | 0x23 | ARS_Modul |
| 1444 | 0x5A4 | Dienste | 36 | 0x24 | CVM_V |
| 1445 | 0x5A5 | Dienste | 37 | 0x25 | RSC_VDA/SC_CT/SC_VDA |
| 1447 | 0x5A7 | Dienste | 39 | 0x27 | PGS |
| 1449 | 0x5A9 | Dienste | 41 | 0x29 | DSC_CT/DSC_RB/DXC_RB |
| 1462 | 0x5B6 | Dienste | 54 | 0x36 | TEL_BPI/TEL_JAP/TEL_MULF |
| 1463 | 0x5B7 | Dienste | 55 | 0x37 | AMP_TOP |
| 1464 | 0x5B8 | Dienste | 56 | 0x38 | EHC |
| 1465 | 0x5B9 | Dienste | 57 | 0x39 | EDCK_Modul |
| 1466 | 0x5BA | Dienste | 58 | 0x3A | KHM |
| 1467 | 0x5BB | Dienste | 59 | 0x3B | JNAV |
| 1468 | 0x5BC | Dienste | 60 | 0x3C | CDC |
| 1469 | 0x5BD | Dienste | 61 | 0x3D | HUD |
| 1472 | 0x5C0 | Dienste | 64 | 0x40 | CAS |
| 1473 | 0x5C1 | Dienste | 65 | 0x41 | DWA |
| 1476 | 0x5C4 | Dienste | 68 | 0x44 | MDS/SHD |
| 1477 | 0x5C5 | Dienste | 69 | 0x45 | RLS/RLS |
| 1483 | 0x5CB | Dienste | 75 | 0x4B | VM |
| 1488 | 0x5D0 | Dienste | 80 | 0x50 | Notstrom-Sirene |
| 1491 | 0x5D3 | Dienste | 83 | 0x53 | IBOC |
| 1492 | 0x5D4 | Dienste | 84 | 0x54 | SDARS |
| 1493 | 0x5D5 | Dienste | 85 | 0x55 | ISpeechBox |
| 1495 | 0x5D7 | Dienste | 87 | 0x57 | NVC |
| 1497 | 0x5D9 | Dienste | 89 | 0x59 | aLBV_FA |
| 1498 | 0x5DA | Dienste | 90 | 0x5A | aLBV_BF |
| 1499 | 0x5DB | Dienste | 91 | 0x5B | DAB |
| 1500 | 0x5DC | Dienste | 92 | 0x5C | Behoerde |
| 1501 | 0x5DD | Dienste | 93 | 0x5D | TLC |
| 1502 | 0x5DE | Dienste | 94 | 0x5E | GWS |
| 1503 | 0x5DF | Dienste | 95 | 0x5F | FLA |
| 1504 | 0x5E0 | Dienste | 96 | 0x60 | Kombi |
| 1506 | 0x5E2 | Dienste | 98 | 0x62 | CCC_GW/M_ASK |
| 1507 | 0x5E3 | Dienste | 99 | 0x63 | CCC_MM |
| 1508 | 0x5E4 | Dienste | 100 | 0x64 | PDC |
| 1509 | 0x5E5 | Dienste | 101 | 0x65 | SZM/SZM_MIT_KBUS |
| 1511 | 0x5E7 | Dienste | 103 | 0x67 | ZBE/ZBE_LO |
| 1515 | 0x5EB | Dienste | 107 | 0x6B | HKL |
| 1517 | 0x5ED | Dienste | 109 | 0x6D | SM_FA/SM_FA_KBUS |
| 1518 | 0x5EE | Dienste | 110 | 0x6E | SM_BF/SM_BF_KBUS |
| 1520 | 0x5F0 | Dienste | 112 | 0x70 | LM/LM_ALC |
| 1521 | 0x5F1 | Dienste | 113 | 0x71 | AHM |
| 1522 | 0x5F2 | Dienste | 114 | 0x72 | KBM |
| 1523 | 0x5F3 | Dienste | 115 | 0x73 | CID_C/CID_C_H |
| 1528 | 0x5F8 | Dienste | 120 | 0x78 | IHKA |
| 1530 | 0x5FA | Dienste | 122 | 0x7A | SH_ZH |
| 1533 | 0x5FD | Dienste | 125 | 0x7D | Diagnosetool_PT_CAN |
| 1534 | 0x5FE | Dienste | 126 | 0x7E | Diagnosetool_K_CAN_System |
| 1545 | 0x609 | Dienste | 137 | 0x89 | Xenon_Scheinwerfer_Links_ALC |
| 1546 | 0x60A | Dienste | 138 | 0x8A | Xenon_Scheinwerfer_Rechts_ALC |
| 1547 | 0x60B | Dienste | 139 | 0x8B | CNV |
| 1649 | 0x671 | Dienste | 241 | 0xF1 | Diagnosedose |
| 4095 | 0xFFF | unbekannt | 255 | 0xFF | Sender unbekannt |
