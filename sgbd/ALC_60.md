# ALC_60.prg

- Jobs: [113](#jobs)
- Tables: [24](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ALC_60 |
| ORIGIN | BMW EI-63 Bilz |
| REVISION | 4.00 |
| AUTHOR | Lear Entwicklung Ahrens |
| COMMENT | SGBD fuer ALC_SG |
| PACKAGE | 1.32 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [CODIERDATEN_BLOCK_LESEN_LEAR](#job-codierdaten-block-lesen-lear) - Auslesen eines Blocks der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block lesen Modus  : Default
- [CODIERDATEN_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten schreiben Modus  : Codieren je nach Block
- [NUR_CODIERDATEN_SCHREIBEN_LEAR](#job-nur-codierdaten-schreiben-lear) - Beschreiben der Default-Codierdaten Format in Datei ohne fuehrende 30 KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten Default schreiben Modus  : Default
- [FLASH_PROG_STATUS_SCHREIBEN_LEAR](#job-flash-prog-status-schreiben-lear) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $02 FlashProgrammierstatus auf 1 setzen Modus  : Default
- [SSECUHVN_SCHREIBEN](#job-ssecuhvn-schreiben) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $93 SystemSupplierECUHardwareVersionNumber Modus  : Default
- [IDENT_SSECUSON](#job-ident-ssecuson) - SystemSupplierECUSoftwareNumber KWP2000: $1A ReadECUIdentification Modus  : SystemSupplierECUSoftwareNumber
- [IDENT_PARAM](#job-ident-param) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : mit Angabe der ID_OPTION zum spezifischen ID_LESEN
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Digitale Inputs
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Analoge Inputs
- [STATUS_CAN_SIGNALE](#job-status-can-signale) - Auslesen der Stati von den CAN-Signalen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 CAN-Signale
- [STATUS_CAN_SIGNALE_TIMEOUT](#job-status-can-signale-timeout) - Auslesen der Stati von den CAN-Signalen-Timeout KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 CAN-Signalen-Timeouts
- [STATUS_BETR_H_ALC](#job-status-betr-h-alc) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Betriebsstunden fuer ALC Status von ALC lesen
- [STEUERN_BETR_H_ALC_LOESCHEN](#job-steuern-betr-h-alc-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Betriebsstunden fuer ALC Status von ALC schreiben
- [READ_ENERGY_SAVING_MODE](#job-read-energy-saving-mode) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [NUR_CODE_IN_EEPROM_SCHREIBEN_LEAR](#job-nur-code-in-eeprom-schreiben-lear) - Beschreiben der Default-Codierdaten Format wird extra erstellt bei Codegenerierung KWP2000: $2E WriteDataByCommonIdentifier $31xx Code in EEPROM schreiben Modus  : Default
- [AUTHENTISIERUNG_EINFACH_LEAR](#job-authentisierung-einfach-lear) - Authentisierung fuer Entwicklung KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication $08 ReleaseAuthentication Modus  : Default
- [NUR_CODIERDATEN_LESEN_LEAR](#job-nur-codierdaten-lesen-lear) - Auslesen der kompletten Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [NUR_CODE_IN_EEPROM_LESEN_LEAR](#job-nur-code-in-eeprom-lesen-lear) - Auslesen des kompletten Codes aus dem EEPROM KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [HERSTELLER_DATEN_SCHREIBEN_LEAR](#job-hersteller-daten-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $0004 Herstellerdaten schreiben
- [HERSTELLER_DATEN_LESEN_LEAR](#job-hersteller-daten-lesen-lear) - Auslesen der Herstellerdaten KWP2000: $22 ReadDataByCommonIdentifier $0004 Herstellerdaten schreiben
- [CBD_ZEICHN_INDEX_LESEN_LEAR](#job-cbd-zeichn-index-lesen-lear) - Auslesen des Aenderungsindex aus den Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [EEPROM_SCHREIBEN_LEAR](#job-eeprom-schreiben-lear) - Beschreiben der Default-Codierdaten (Codierdaten und Code im EEPROM) KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten schreiben $31xx Code in EEPROM schreiben Modus  : Default
- [STEUERN_SMC_BESTROMEN](#job-steuern-smc-bestromen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $01 SMC bestromen Status von LM-E65 schreiben
- [CODIERDATEN_SMC_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-smc-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier $xxxx Codierdaten schreiben Modus  : Codieren je nach Block
- [CODIERDATEN_SMC_SCHREIBEN_LEAR](#job-codierdaten-smc-schreiben-lear) - Beschreiben der Default-Codierdaten KWP 2000:$A6 LINGateway $2E WriteDataByCommonIdentifier $32xx Codierdaten SMC links schreiben $33xx Codierdaten SMC rechts schreiben Modus  : Default
- [CODIERDATEN_SMC_BLOCK_LESEN_LEAR](#job-codierdaten-smc-block-lesen-lear) - Auslesen der Codierdaten fuer einen Block KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x32xx Codierdaten SMC links schreiben $0x33xx Codierdaten SMC rechts schreiben Modus  : Default
- [CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-links-lesen-komplett-lear) - Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $32xx Codierdaten SMC links lesen Modus  : Default
- [CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-rechts-lesen-komplett-lear) - Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $33xx Codierdaten SMC rechts lesen Modus  : Default
- [VIN_SMC_LINKS_SCHREIBEN_LEAR](#job-vin-smc-links-schreiben-lear) - Schreiben der VIN in die linke SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN
- [VIN_SMC_RECHTS_SCHREIBEN_LEAR](#job-vin-smc-rechts-schreiben-lear) - Schreiben der VIN in die rechte SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN
- [VIN_SMC_LESEN](#job-vin-smc-lesen) - Fahrgestellnummer fuer SMC links und rechts lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [ID_SMC_LESEN](#job-id-smc-lesen) - ID-SMC lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-SMC Modus  : Default
- [STEUERN_REFERENZLAUF_SMC](#job-steuern-referenzlauf-smc) - Referenzlauf der SMC starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten
- [STATUS_POSITION_SMC](#job-status-position-smc) - IST-Position der SMC auslesen KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR
- [STEUERN_POSITION_SMC](#job-steuern-position-smc) - bestimmte Position der SMC anfahren KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht starten $41 Pos LWR starten
- [SMC_SPEICHER_LESEN_LEAR](#job-smc-speicher-lesen-lear) - Speicher lesen KWP 2000: $A6 LINGateway $23 ReadMemoryByAddress Modus  : Default
- [SMC_SPEICHER_SCHREIBEN_LEAR](#job-smc-speicher-schreiben-lear) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Start-Adresse Datenbyte KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [HERSTELLERDATEN_SMC_LEAR_SCHREIBEN](#job-herstellerdaten-smc-lear-schreiben) - Beschreiben der LEAR-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [HERSTELLERDATEN_SMC_LEAR_LESEN](#job-herstellerdaten-smc-lear-lesen) - Auslesen der LEAR-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3280 Herstellerdaten SMC links lesen $0x3380 HErstellerdaten SMC rechts lesen Modus  : Default
- [HERSTELLERDATEN_SMC_SCHEINWERFER_SCHREIBEN](#job-herstellerdaten-smc-scheinwerfer-schreiben) - Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [HERSTELLERDATEN_SMC_SCHEINWERFER_LESEN](#job-herstellerdaten-smc-scheinwerfer-lesen) - Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default
- [IS_LESEN_SMC_L_LEAR](#job-is-lesen-smc-l-lear) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_SMC_R_LEAR](#job-is-lesen-smc-r-lear) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL_SMC_L_LEAR](#job-is-lesen-detail-smc-l-lear) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LESEN_DETAIL_SMC_R_LEAR](#job-is-lesen-detail-smc-r-lear) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN_SMC_L_LEAR](#job-is-loeschen-smc-l-lear) - Infospeicher loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [IS_LOESCHEN_SMC_R_LEAR](#job-is-loeschen-smc-r-lear) - Infospeicher loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [STATUS_BETR_H_SMC](#job-status-betr-h-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $51 Betriebsstunden Status von SMC lesen
- [STEUERN_BETR_H_SMC_LOESCHEN](#job-steuern-betr-h-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $51 Betriebsstunden
- [STATUS_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC](#job-status-verteilung-winkel-ansteuerung-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $50 Verteilung der Winkelansteuerung Status von SMC lesen
- [STEUERN_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC_LOESCHEN](#job-steuern-verteilung-winkel-ansteuerung-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $50 Verteilung der Winkelansteuerung
- [STATUS_TEMPERATURVERTEILUNG_SMC](#job-status-temperaturverteilung-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $52 Temperaturverteilung Status von SMC lesen
- [STEUERN_TEMPERATURVERTEILUNG_SMC_LOESCHEN](#job-steuern-temperaturverteilung-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $52 Temperaturverteilung
- [STATUS_SCHRITTVERLUSTE_SMC](#job-status-schrittverluste-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $53 Schrittverluste Status von SMC lesen
- [STEUERN_SCHRITTVERLUSTE_SMC_LOESCHEN](#job-steuern-schrittverluste-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $53 Schrittverluste
- [STATUS_HW_EINGANGE_SMC](#job-status-hw-eingange-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $54 HW_Eingaenge Status von SMC lesen
- [HERSTELLERTEST_SMC_LEAR](#job-herstellertest-smc-lear) - Herstellertest KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $04 Herstellertest Modus  : Default
- [SCHEINWERFERHERSTELLERDATEN_SCHREIBEN](#job-scheinwerferherstellerdaten-schreiben) - Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [SCHEINWERFERHERSTELLERDATEN_LESEN](#job-scheinwerferherstellerdaten-lesen) - Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default
- [PRUEFSTEMPEL_SCHEINWERFER_SCHREIBEN](#job-pruefstempel-scheinwerfer-schreiben) - Beschreiben des Scheinwerfer-Pruefstempel KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [PRUEFSTEMPEL_SCHEINWERFER_LESEN](#job-pruefstempel-scheinwerfer-lesen) - Auslesen der Scheinwerfer-Pruefstempel KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Scheinwerfer-Pruefstempel SMC links lesen $0x3381 Scheinwerfer-Pruefstempel SMC rechts lesen Modus  : Default

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

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-codierdaten-block-lesen-lear"></a>
### CODIERDATEN_BLOCK_LESEN_LEAR

Auslesen eines Blocks der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Bereich: 0x30xx und 0x31xx |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | binary | Codierdaten fuer angegebenen Block |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-block-schreiben-lear"></a>
### CODIERDATEN_BLOCK_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten schreiben Modus  : Codieren je nach Block

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | Block+Codierdaten Block+Codierdaten (z.B. 300001020304...) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nur-codierdaten-schreiben-lear"></a>
### NUR_CODIERDATEN_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten Format in Datei ohne fuehrende 30 KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten Default schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-prog-status-schreiben-lear"></a>
### FLASH_PROG_STATUS_SCHREIBEN_LEAR

Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $02 FlashProgrammierstatus auf 1 setzen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ssecuhvn-schreiben"></a>
### SSECUHVN_SCHREIBEN

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $93 SystemSupplierECUHardwareVersionNumber Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ssecuson"></a>
### IDENT_SSECUSON

SystemSupplierECUSoftwareNumber KWP2000: $1A ReadECUIdentification Modus  : SystemSupplierECUSoftwareNumber

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SW_APP | string | SystemSupplierECUSoftwareNumber fuer Applikation |
| ID_SW_BOOT | string | SystemSupplierECUSoftwareNumber fuer Bootloader |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-param"></a>
### IDENT_PARAM

Identdaten KWP2000: $1A ReadECUIdentification Modus  : mit Angabe der ID_OPTION zum spezifischen ID_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID_OPT | int | Bereich: 0x86-0x9F |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR_1 | string | BMW-Teilenummer 1.Eintrag |
| ID_BMW_NR_2 | string | BMW-Teilenummer 2.Eintrag |
| ID_BMW_NR_3 | string | BMW-Teilenummer 3.Eintrag |
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
| ID_CHANGE_INDEX | string | Change-Index |
| ID_SSECUSEN | string | SystenSupplierECUSerialNumber |
| ID_VIN | string | VehicleIdentificationNumber |
| ID_SSECUHN | string | SystemSupplierECUHardwareNumber |
| ID_SSECUHVN | string | SystemSupplierECUHardwareVersionNumber |
| ID_SSECUSON | string | SystemSupplierECUSoftwareNumber |
| ID_SSECUSVN | string | SystemSupplierECUSoftwareVersionNumber |
| ID_PD | string | ProgrammingDate |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Digitale Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WAKELEITUNG_EIN | int | CAN-HW-Wakeleitung |
| STAT_S_BL_EIN | int | Bremslichtschalter |
| STAT_S_RUECKW_GANG_EIN | int | Rueckwaertsgang ein |
| STAT_S_DUMMY_EIN | int | unbelegt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-inputs"></a>
### STATUS_ANALOG_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Analoge Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_WERT | real | Spannung Sensor Hoehenstandsmesser vorne Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_HINTEN_WERT | real | Spannung Sensor Hoehenstandsmesser hinten Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_KLEMME_30A_WERT | real | Spannung Klemme 30A Bereich: 0 V bis 25 V |
| STAT_SPANNUNG_S_BL_WERT | real | Spannung Bremslichtschalter Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_VERSORGUNG_SMC_WERT | real | Spannungsversorgung SMC Bereich: 0 V bis 25 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-signale"></a>
### STATUS_CAN_SIGNALE

Auslesen der Stati von den CAN-Signalen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 CAN-Signale

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKWINKEL_WERT | int |  |
| STAT_GESCHWINDIGKEIT_WERT | unsigned int |  |
| STAT_GIERRATE_WERT | int |  |
| STAT_ABBLENDLICHT_WERT | unsigned char |  |
| STAT_POSITIONSLICHT_WERT | unsigned char |  |
| STAT_CONTROL_ALC_WERT | unsigned char |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-signale-timeout"></a>
### STATUS_CAN_SIGNALE_TIMEOUT

Auslesen der Stati von den CAN-Signalen-Timeout KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 CAN-Signalen-Timeouts

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INSTR3_CAN_11H_EIN | int |  |
| STAT_EGS1_CAN_11H_EIN | int |  |
| STAT_GANG_RUECKWAERTS_EIN | int |  |
| STAT_CTR_ALC_EIN | int |  |
| STAT_DME2_CAN_11H_EIN | int |  |
| STAT_DME1_CAN_11H_EIN | int |  |
| STAT_A_TEMP_RELATIVZEIT_EIN | int |  |
| STAT_LAMPENZUSTAND_EIN | int |  |
| STAT_LWS1_CAN_11H_EIN | int |  |
| STAT_ASC3_CAN_11H_EIN | int |  |
| STAT_ENGINE_1_EIN | int |  |
| STAT_GESCHWINDIGKEIT_EIN | int |  |
| STAT_STAT_DSC_EIN | int |  |
| STAT_ASC1_CAN_11H_EIN | int |  |
| STAT_KLEMMENSTATUS_EIN | int |  |
| STAT_LENKRADWINKEL_EIN | int |  |
| STAT_GETRIEBEDATEN_EIN | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-alc"></a>
### STATUS_BETR_H_ALC

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Betriebsstunden fuer ALC Status von ALC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_ALC_WERT | real | Betriebsstunden ALC auslesen |
| STAT_BETRIEBSZEIT_SCHWENKEN_WERT | real | Betriebsstunden Schwenken aktiv auslesen |
| STAT_BETRIEBSZEIT_SMC_BESTROMT_WERT | real | Betriebsstunden SMCs bestromt auslesen |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebszeit [min] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-alc-loeschen"></a>
### STEUERN_BETR_H_ALC_LOESCHEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Betriebsstunden fuer ALC Status von ALC schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-saving-mode"></a>
### READ_ENERGY_SAVING_MODE

Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ENERGY_SAVING_MODE | string | Ausgabe des Engery-Saving-Modes |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nur-code-in-eeprom-schreiben-lear"></a>
### NUR_CODE_IN_EEPROM_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten Format wird extra erstellt bei Codegenerierung KWP2000: $2E WriteDataByCommonIdentifier $31xx Code in EEPROM schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit generiertem Code Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.cod codiert letztes Zeichen muss ein LF sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-einfach-lear"></a>
### AUTHENTISIERUNG_EINFACH_LEAR

Authentisierung fuer Entwicklung KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication $08 ReleaseAuthentication Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nur-codierdaten-lesen-lear"></a>
### NUR_CODIERDATEN_LESEN_LEAR

Auslesen der kompletten Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | die kompletten Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nur-code-in-eeprom-lesen-lear"></a>
### NUR_CODE_IN_EEPROM_LESEN_LEAR

Auslesen des kompletten Codes aus dem EEPROM KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| COD_COD_LEN | int | Laenge der Code-Codierdaten |
| COD_CHECK_SUM | string | Checksumme der Code-Codierdaten |
| LAND | string | Land |
| EXT | string | Extension |
| COD_INDEX | int | Codierindex |
| COD_VARIANTE | int | Codiervariante |
| CODE_DATEN_1 | string | Teil 1 der kompletten Code-Codierdaten |
| CODE_DATEN_2 | string | Teil 2 der kompletten Code-Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-schreiben-lear"></a>
### HERSTELLER_DATEN_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $0004 Herstellerdaten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Block+Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-lesen-lear"></a>
### HERSTELLER_DATEN_LESEN_LEAR

Auslesen der Herstellerdaten KWP2000: $22 ReadDataByCommonIdentifier $0004 Herstellerdaten schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HERSTELLERDATEN | binary | Herstellerdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbd-zeichn-index-lesen-lear"></a>
### CBD_ZEICHN_INDEX_LESEN_LEAR

Auslesen des Aenderungsindex aus den Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CBD_ZEICHN_INDEX | string | Aenderungsindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-eeprom-schreiben-lear"></a>
### EEPROM_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten (Codierdaten und Code im EEPROM) KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten schreiben $31xx Code in EEPROM schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-smc-bestromen"></a>
### STEUERN_SMC_BESTROMEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $01 SMC bestromen Status von LM-E65 schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BESTROMEN_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-block-schreiben-lear"></a>
### CODIERDATEN_SMC_BLOCK_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier $xxxx Codierdaten schreiben Modus  : Codieren je nach Block

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | Block+Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-schreiben-lear"></a>
### CODIERDATEN_SMC_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten KWP 2000:$A6 LINGateway $2E WriteDataByCommonIdentifier $32xx Codierdaten SMC links schreiben $33xx Codierdaten SMC rechts schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-block-lesen-lear"></a>
### CODIERDATEN_SMC_BLOCK_LESEN_LEAR

Auslesen der Codierdaten fuer einen Block KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x32xx Codierdaten SMC links schreiben $0x33xx Codierdaten SMC rechts schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Bereich: 30xx und 31xx |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-links-lesen-komplett-lear"></a>
### CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $32xx Codierdaten SMC links lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_1 | string | Teil 1 der kompletten Codierdaten |
| CODIERDATEN_2 | string | Teil 2 der kompletten Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-rechts-lesen-komplett-lear"></a>
### CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $33xx Codierdaten SMC rechts lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_1 | string | Teil 1 der kompletten Codierdaten |
| CODIERDATEN_2 | string | Teil 2 der kompletten Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vin-smc-links-schreiben-lear"></a>
### VIN_SMC_LINKS_SCHREIBEN_LEAR

Schreiben der VIN in die linke SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VINDATEN | string | 7stellige VIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vin-smc-rechts-schreiben-lear"></a>
### VIN_SMC_RECHTS_SCHREIBEN_LEAR

Schreiben der VIN in die rechte SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VINDATEN | string | 7stellige VIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vin-smc-lesen"></a>
### VIN_SMC_LESEN

Fahrgestellnummer fuer SMC links und rechts lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VIN_SMC_LINKS | string | Fahrgestellnummer 7-stellig fuer SMC links |
| VIN_SMC_LINKS_KONFIG | int | Konfigbyte Fahrgestellnummer fuer SMC links |
| VIN_SMC_RECHTS | string | Fahrgestellnummer 7-stellig fuer SMC rechts |
| VIN_SMC_RECHTS_KONFIG | int | Konfigbyte Fahrgestellnummer fuer SMC rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-id-smc-lesen"></a>
### ID_SMC_LESEN

ID-SMC lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-SMC Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_VERSION_SMC_LINKS | string | SW-Version fuer SMC links |
| HW_VERSION_SMC_LINKS | string | HW-Version fuer SMC links |
| CODING_INDEX_SMC_LINKS | string | Codierindex fuer SMC links |
| MCV_VERSION_SMC_LINKS | string | MCV-Version fuer SMC links |
| SW_VERSION_SMC_RECHTS | string | SW-Version fuer SMC rechts |
| HW_VERSION_SMC_RECHTS | string | HW-Version fuer SMC rechts |
| CODING_INDEX_SMC_RECHTS | string | Codierindex fuer SMC rechts |
| MCV_VERSION_SMC_RECHTS | string | MCV-Version fuer SMC rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-referenzlauf-smc"></a>
### STEUERN_REFERENZLAUF_SMC

Referenzlauf der SMC starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| REFERENZLAUF | string | Referenzlauf auswaehlen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-position-smc"></a>
### STATUS_POSITION_SMC

IST-Position der SMC auslesen KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POS_KURVENLICHT | long | Winkel fuer Kurvenlicht |
| STAT_POS_LWR | long | Winkel fuer LWR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-smc"></a>
### STEUERN_POSITION_SMC

bestimmte Position der SMC anfahren KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht starten $41 Pos LWR starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| POS_KURVENLICHT | long | Winkel fuer Kurvenlicht |
| GESCHW_KURVENLICHT | unsigned char | Geschwindigkeit fuer Kurvenlicht |
| POS_LWR | long | Winkel fuer LWR |
| GESCHW_LWR | unsigned char | Geschwindigkeit fuer LWR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-smc-speicher-lesen-lear"></a>
### SMC_SPEICHER_LESEN_LEAR

Speicher lesen KWP 2000: $A6 LINGateway $23 ReadMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| ADRESSE | long | zu lesende Adresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-smc-speicher-schreiben-lear"></a>
### SMC_SPEICHER_SCHREIBEN_LEAR

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Start-Adresse Datenbyte KWP2000: $3D WriteMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| DATEN | string | zu schreibende Daten (immer 1 Byte) z.B. 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-lear-schreiben"></a>
### HERSTELLERDATEN_SMC_LEAR_SCHREIBEN

Beschreiben der LEAR-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-lear-lesen"></a>
### HERSTELLERDATEN_SMC_LEAR_LESEN

Auslesen der LEAR-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3280 Herstellerdaten SMC links lesen $0x3380 HErstellerdaten SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-scheinwerfer-schreiben"></a>
### HERSTELLERDATEN_SMC_SCHEINWERFER_SCHREIBEN

Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-scheinwerfer-lesen"></a>
### HERSTELLERDATEN_SMC_SCHEINWERFER_LESEN

Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-smc-l-lear"></a>
### IS_LESEN_SMC_L_LEAR

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

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

<a id="job-is-lesen-smc-r-lear"></a>
### IS_LESEN_SMC_R_LEAR

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

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

<a id="job-is-lesen-detail-smc-l-lear"></a>
### IS_LESEN_DETAIL_SMC_L_LEAR

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

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

<a id="job-is-lesen-detail-smc-r-lear"></a>
### IS_LESEN_DETAIL_SMC_R_LEAR

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

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

<a id="job-is-loeschen-smc-l-lear"></a>
### IS_LOESCHEN_SMC_L_LEAR

Infospeicher loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen-smc-r-lear"></a>
### IS_LOESCHEN_SMC_R_LEAR

Infospeicher loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-smc"></a>
### STATUS_BETR_H_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $51 Betriebsstunden Status von SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_SMC_WERT | unsigned long | Betr_h SMC |
| STAT_RESETCOUNTER_WERT | unsigned long | Anzahl Resets |
| STAT_ANZ_HS_KURVENLICHT_WERT | unsigned long | Anzahl Halbschritte Kurvenlicht |
| STAT_ANZ_HS_LWR_WERT | unsigned long | Anzahl Halbschritte LWR |
| STAT_ACHSEN_VERFAHRZEIT_KURVENLICHT_WERT | unsigned long | Achsenverfahrzeit fuer Kurvenlicht |
| STAT_ACHSEN_VERFAHRZEIT_LWR_WERT | unsigned long | Achsenverfahrzeit fur LWR |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebsstunden |
| STAT_VERFAHRZEIT_EINH | string | Einheit fuer Achsenverfahrzeit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-smc-loeschen"></a>
### STEUERN_BETR_H_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $51 Betriebsstunden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verteilung-winkel-ansteuerung-smc"></a>
### STATUS_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $50 Verteilung der Winkelansteuerung Status von SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WINKEL_0_2_WERT | unsigned int | WINKEL zwischen 0° und 2° |
| STAT_WINKEL_2_4_WERT | unsigned int | WINKEL zwischen 2° und 4° |
| STAT_WINKEL_4_6_WERT | unsigned int | WINKEL zwischen 4° und 6° |
| STAT_WINKEL_6_8_WERT | unsigned int | WINKEL zwischen 6° und 8° |
| STAT_WINKEL_8_10_WERT | unsigned int | WINKEL zwischen 8° und 10° |
| STAT_WINKEL_10_12_WERT | unsigned int | WINKEL zwischen 10° und 12° |
| STAT_WINKEL_12_14_WERT | unsigned int | WINKEL zwischen 12° und 14° |
| STAT_WINKEL_14_16_WERT | unsigned int | WINKEL zwischen 14° und 16° |
| STAT_WINKEL_MINUS_0_2_WERT | unsigned int | WINKEL zwischen 0° und -2° |
| STAT_WINKEL_MINUS_2_4_WERT | unsigned int | WINKEL zwischen -2° und -4° |
| STAT_WINKEL_MINUS_4_6_WERT | unsigned int | WINKEL zwischen -4° und -6° |
| STAT_WINKEL_MINUS_6_8_WERT | unsigned int | WINKEL zwischen -6° und -8° |
| STAT_WINKEL_MINUS_8_10_WERT | unsigned int | WINKEL zwischen -8° und -10° |
| STAT_WINKEL_MINUS_10_12_WERT | unsigned int | WINKEL zwischen -10° und -12° |
| STAT_WINKEL_MINUS_12_14_WERT | unsigned int | WINKEL zwischen -12° und -14° |
| STAT_WINKEL_MINUS_14_16_WERT | unsigned int | WINKEL zwischen -14° und -16° |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-verteilung-winkel-ansteuerung-smc-loeschen"></a>
### STEUERN_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $50 Verteilung der Winkelansteuerung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperaturverteilung-smc"></a>
### STATUS_TEMPERATURVERTEILUNG_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $52 Temperaturverteilung Status von SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_10_PROZENT_ABSCHALTUNG_WERT | unsigned int | 10% werden nicht mehr angefahren |
| STAT_20_PROZENT_ABSCHALTUNG_WERT | unsigned int | 20% werden nicht mehr angefahren |
| STAT_30_PROZENT_ABSCHALTUNG_WERT | unsigned int | 30% werden nicht mehr angefahren |
| STAT_40_PROZENT_ABSCHALTUNG_WERT | unsigned int | 40% werden nicht mehr angefahren |
| STAT_50_PROZENT_ABSCHALTUNG_WERT | unsigned int | 50% werden nicht mehr angefahren |
| STAT_60_PROZENT_ABSCHALTUNG_WERT | unsigned int | 60% werden nicht mehr angefahren |
| STAT_70_PROZENT_ABSCHALTUNG_WERT | unsigned int | 70% werden nicht mehr angefahren |
| STAT_80_PROZENT_ABSCHALTUNG_WERT | unsigned int | 80% werden nicht mehr angefahren |
| STAT_90_PROZENT_ABSCHALTUNG_WERT | unsigned int | 90% werden nicht mehr angefahren |
| STAT_100_PROZENT_ABSCHALTUNG_WERT | unsigned int | 100% werden nicht mehr angefahren |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-temperaturverteilung-smc-loeschen"></a>
### STEUERN_TEMPERATURVERTEILUNG_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $52 Temperaturverteilung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schrittverluste-smc"></a>
### STATUS_SCHRITTVERLUSTE_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $53 Schrittverluste Status von SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHRITTVERLUSTGRENZE_1_WERT | unsigned int | Schrittverluste in Bereich 1 |
| STAT_SCHRITTVERLUSTGRENZE_2_WERT | unsigned int | Schrittverluste in Bereich 2 |
| STAT_SCHRITTVERLUSTGRENZE_3_WERT | unsigned int | Schrittverluste in Bereich 3 |
| STAT_SCHRITTVERLUSTGRENZE_4_WERT | unsigned int | Schrittverluste in Bereich 4 |
| STAT_SCHRITTVERLUSTGRENZE_5_WERT | unsigned int | Schrittverluste in Bereich 5 |
| STAT_SCHRITTVERLUSTGRENZE_6_WERT | unsigned int | Schrittverluste in Bereich 6 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schrittverluste-smc-loeschen"></a>
### STEUERN_SCHRITTVERLUSTE_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $53 Schrittverluste

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-eingange-smc"></a>
### STATUS_HW_EINGANGE_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $54 HW_Eingaenge Status von SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_U_BATT_WERT | unsigned int | Batteriespannung |
| STAT_SPANNUNG_BATT_WERT | real | Batteriespannung Bereich: 0 .. 18 Volt |
| STAT_U_KOD_WERT | unsigned int | Kodierspannung: kleiner 128: SMC_L, groesser 128: SMC_R |
| STAT_U_SENSE_WERT | unsigned int | Sensespannung |
| STAT_SPANNUNG_SENSE_WERT | real | Sensespannung Bereich: 0 .. 5 Volt |
| STAT_COD_1_EIN | unsigned int | Hardwarekodierungseingang 1 |
| STAT_COD_2_EIN | unsigned int | Hardwarekodierungseingang 2 |
| STAT_COD_3_EIN | unsigned int | Hardwarekodierungseingang 3 |
| STAT_SENSE_UP_DOWN_EIN | unsigned int | Zustand von Sensor-Pullup |
| STAT_U_SENSE_EIN | unsigned int | Sensorspannung ein |
| STAT_KONTROLL_WERT | unsigned long | Sensor Kontrollwert: Anzahl HS der letzten Schrittverluste |
| STAT_SENSOR_WERT | unsigned long | Sensorwert PWM-Verhaeltnis |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellertest-smc-lear"></a>
### HERSTELLERTEST_SMC_LEAR

Herstellertest KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $04 Herstellertest Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| UBAT_HIGH | unsigned char | Grenzwert Batteriespannung Highwert |
| UBAT_LOW | unsigned char | Grenzwert Batteriespannung Lowwert |
| USEN_HIGH | unsigned char | Grenzwert Sensespannung Highwert |
| USEN_LOW | unsigned char | Grenzwert Sensespannung Lowwert |
| DIGITAL_MASK_1 | unsigned char | Musterbyte fuer Digitalstatus 1 |
| DIGITAL_MASK_2 | unsigned char | Musterbyte fuer Digitalstatus 2 |
| DIGITAL_MASK_3 | unsigned char | Musterbyte fuer Digitalstatus 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS | string | Statusbyte |
| UBAT_1 | real | Batteriespannung 1 |
| UBAT_2 | real | Batteriespannung 2 |
| UBAT_3 | real | Batteriespannung 3 |
| USEN_1 | real | Sensespannung 1 |
| USEN_2 | real | Sensespannung 2 |
| USEN_3 | real | Sensespannung 3 |
| DIGITAL_1 | string | Digitalwerte Satz 1 |
| DIGITAL_2 | string | Digitalwerte Satz 2 |
| DIGITAL_3 | string | Digitalwerte Satz 3 |
| HERSTELLERTEST | string | Daten Herstellertest |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-scheinwerferherstellerdaten-schreiben"></a>
### SCHEINWERFERHERSTELLERDATEN_SCHREIBEN

Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| SCHEINWERFER_HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-scheinwerferherstellerdaten-lesen"></a>
### SCHEINWERFERHERSTELLERDATEN_LESEN

Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHEINWERFER_HERSTELLERDATEN | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-scheinwerfer-schreiben"></a>
### PRUEFSTEMPEL_SCHEINWERFER_SCHREIBEN

Beschreiben des Scheinwerfer-Pruefstempel KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| SCHEINWERFER_PRUEFSTEMPEL | string | Scheinwerfer-Pruefstempel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-scheinwerfer-lesen"></a>
### PRUEFSTEMPEL_SCHEINWERFER_LESEN

Auslesen der Scheinwerfer-Pruefstempel KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Scheinwerfer-Pruefstempel SMC links lesen $0x3381 Scheinwerfer-Pruefstempel SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHEINWERFER_PRUEFSTEMPEL | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FORTTEXTE](#table-forttexte) (17 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IORTTEXTE](#table-iorttexte) (48 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (44 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (11 × 9)
- [NOTL](#table-notl) (1 × 7)
- [READVARIABLE](#table-readvariable) (7 × 3)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [SMCS](#table-smcs) (3 × 3)
- [REF_SMCS](#table-ref-smcs) (4 × 3)

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

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 17 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA588 | interner Fehler ALC-SG |
| 0xA589 | Kommunikation mit StepperMoterBox 1 gestoert |
| 0xA58A | Kommunikation mit StepperMoterBox 2 gestoert |
| 0xA58B | Sensor Hoehenstand vorne defekt |
| 0xA58C | Sensor Hoehenstand hinten defekt |
| 0xA58D | Bremslichtschalter defekt |
| 0xA58E | Energiesparmode aktiv |
| 0xA58F | Fehler WAKE-Leitung |
| 0xA590 | Achtung: Elektronik am linken Scheinwerfer (SMC) meldet Fehler |
| 0xA591 | Achtung: Elektronik am rechten Scheinwerfer (SMC) meldet Fehler |
| 0xA592 | Vergleich Fahrgestellnummer ALC mit SMC links unterschiedlich |
| 0xA593 | Vergleich Fahrgestellnummer ALC mit SMC rechts unterschiedlich |
| 0xA594 | neuer Fehler 1 |
| 0xA595 | neuer Fehler 2 |
| 0xA596 | neuer Fehler 3 |
| 0xD187 | Controller, Bus Off |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 48 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | EEPROM SMC links defekt |
| 0x9309 | Motor Kurvenlicht SMC links defekt |
| 0x930A | Motor LWR SMC links defekt |
| 0x930B | Treiber Kurvenlicht SMC links defekt |
| 0x930C | Spannungsversorgung Sensor SMC links defekt |
| 0x930D | Signal Sensor SMC links defekt |
| 0x930E | Flanke Sensor SMC links defekt |
| 0x930F | LIN SMC links defekt |
| 0x9310 | Schrittverlust Grenze 1 SMC links |
| 0x9311 | Schrittverlust Grenze 2 SMC links |
| 0x9312 | Schrittverlust Grenze 3 SMC links |
| 0x9313 | Schrittverlust Grenze 4 SMC links |
| 0x9314 | Schrittverlust Grenze 5 SMC links |
| 0x9315 | Schrittverlust Grenze 6 SMC links |
| 0x9316 | Spike auf Sensor SMS links |
| 0x9317 | Notlauf aktiv SMC links |
| 0x9318 | unbekannter Fehler 2 SMC links |
| 0x9319 | unbekannter Fehler 3 SMC links |
| 0x931A | unbekannter Fehler 4 SMC links |
| 0x931B | unbekannter Fehler 5 SMC links |
| 0x931C | EEPROM SMC rechts defekt |
| 0x931D | Motor Kurvenlicht SMC rechts defekt |
| 0x931E | Motor LWR SMC rechts defekt |
| 0x931F | Treiber Kurvenlicht SMC rechts defekt |
| 0x9320 | Spannungsversorgung Sensor SMC rechts defekt |
| 0x9321 | Signal Sensor SMC rechts defekt |
| 0x9322 | Flanke Sensor SMC rechts defekt |
| 0x9323 | LIN SMC rechts defekt |
| 0x9324 | Schrittverlust Grenze 1 SMC rechts |
| 0x9325 | Schrittverlust Grenze 2 SMC rechts |
| 0x9326 | Schrittverlust Grenze 3 SMC rechts |
| 0x9327 | Schrittverlust Grenze 4 SMC rechts |
| 0x9328 | Schrittverlust Grenze 5 SMC rechts |
| 0x9329 | Schrittverlust Grenze 6 SMC rechts |
| 0x932A | Spike auf Sensor SMS rechts |
| 0x932B | Notlauf aktiv SMC rechts |
| 0x932C | unbekannter Fehler 2 SMC rechts |
| 0x932D | unbekannter Fehler 3 SMC rechts |
| 0x932E | unbekannter Fehler 4 SMC rechts |
| 0x932F | unbekannter Fehler 5 SMC rechts |
| 0x9330 | Telegramm Geschwindigkeit ungueltig |
| 0x9331 | Telegramm Gierrate Timeout oder ungueltig |
| 0x9332 | Telegramm Lenkwinkel Timeout oder ungueltig |
| 0x9333 | Telegramm Lampenzustand Timeout oder ungueltig |
| 0x9334 | Telegramm Klemmenstatus Timeout oder ungueltig |
| 0x9335 | Telegramm Steuerung ALC Timeout oder ungueltig |
| 0x9336 | ALC meldet Fehler an Lichtmodul |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 44 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9308 | 0x03 | -- | -- | -- |
| 0x9309 | 0x01 | -- | -- | -- |
| 0x930A | 0x01 | -- | -- | -- |
| 0x930B | 0x01 | -- | -- | -- |
| 0x930C | 0x02 | -- | -- | -- |
| 0x930D | 0x01 | -- | -- | -- |
| 0x930E | 0x01 | -- | -- | -- |
| 0x930F | 0x01 | -- | -- | -- |
| 0x9310 | 0x01 | -- | -- | -- |
| 0x9311 | 0x01 | -- | -- | -- |
| 0x9312 | 0x01 | -- | -- | -- |
| 0x9313 | 0x01 | -- | -- | -- |
| 0x9314 | 0x01 | -- | -- | -- |
| 0x9315 | 0x01 | -- | -- | -- |
| 0x9316 | 0x02 | -- | -- | -- |
| 0x9317 | NOTL | -- | -- | -- |
| 0x9318 | -- | -- | -- | -- |
| 0x9319 | -- | -- | -- | -- |
| 0x931A | -- | -- | -- | -- |
| 0x931B | -- | -- | -- | -- |
| 0x931C | 0x03 | -- | -- | -- |
| 0x931D | 0x01 | -- | -- | -- |
| 0x931E | 0x01 | -- | -- | -- |
| 0x931F | 0x01 | -- | -- | -- |
| 0x9320 | 0x02 | -- | -- | -- |
| 0x9321 | 0x01 | -- | -- | -- |
| 0x9322 | 0x01 | -- | -- | -- |
| 0x9323 | 0x01 | -- | -- | -- |
| 0x9324 | 0x01 | -- | -- | -- |
| 0x9325 | 0x01 | -- | -- | -- |
| 0x9326 | 0x01 | -- | -- | -- |
| 0x9327 | 0x01 | -- | -- | -- |
| 0x9328 | 0x01 | -- | -- | -- |
| 0x9329 | 0x01 | -- | -- | -- |
| 0x932A | 0x02 | -- | -- | -- |
| 0x932B | NOTL | -- | -- | -- |
| 0x932C | -- | -- | -- | -- |
| 0x932D | -- | -- | -- | -- |
| 0x932E | -- | -- | -- | -- |
| 0x932F | -- | -- | -- | -- |
| 0x9330 | 0x04 | -- | -- | -- |
| 0x9331 | 0x04 | -- | -- | -- |
| 0x9332 | 0x04 | -- | -- | -- |
| 0x9333 | 0x04 | -- | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 11 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | -- | unsigned char | -- |  18 | 255 | 0 |
| 0x02 | Sensorspannung | Volt | -- | unsigned char | -- |  5 | 255 | 0 |
| 0x03 | Motortemperatur | °C | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x04 | Bordnetzspannung | Volt | -- | unsigned char | -- |  25 | 255 | 0 |
| 0x10 | NOT_SENS_DEFEKT | 0/1 | high | 0x01 | - | - | - | - |
| 0x11 | NOT_SENS_NOK | 0/1 | high | 0x02 | - | - | - | - |
| 0x12 | NOT_SCHR_VER_NOK | 0/1 | high | 0x04 | - | - | - | - |
| 0x13 | NOT_USENS_NOK | 0/1 | high | 0x08 | - | - | - | - |
| 0x14 | NOT_MOTOR_DEF | 0/1 | high | 0x10 | - | - | - | - |
| 0x15 | NOT_MOTOR_LWR_DEF | 0/1 | high | 0x20 | - | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-notl"></a>
### NOTL

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 |

<a id="table-readvariable"></a>
### READVARIABLE

Dimensions: 7 rows × 3 columns

| VARNR | NAME | TEXT |
| --- | --- | --- |
| 0x00 | FLAGS_FLAGS | flags.flags |
| 0x01 | FLAGS_ANFORD | flags.anforderung |
| 0x02 | FLAGS_CAN_ANFORDERUNG | flags.can_anforderung |
| 0x03 | LAMPEN_FEHLER_FLAGS | lampen_fehler.flags |
| 0x04 | LAMPEN_FEHLER_ZAEHLER | lampen_fehler.zaehler |
| 0x05 | TEST_ATD | test_ATD |
| 0x06 | UNKNOWN | unbekannte Variable |

<a id="table-energysaving"></a>
### ENERGYSAVING

Dimensions: 5 rows × 3 columns

| E_MODE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | ENERGY_MODE_AUS | Energysaving aus |
| 0x01 | ENERGY_MODE_PRODUCTION | Energysaving Produktion |
| 0x02 | ENERGY_MODE_SHIPMENT | Energysaving Shipment |
| 0x04 | ENERGY_MODE_REPAIR_SHOP | Energysaving Repair-Shop |
| 0x08 | ERROR | falscher Eingabewert |

<a id="table-smcs"></a>
### SMCS

Dimensions: 3 rows × 3 columns

| SMC | NAME | TEXT |
| --- | --- | --- |
| 0x89 | SMC_L | SMC links |
| 0x8A | SMC_R | SMC rechts |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-ref-smcs"></a>
### REF_SMCS

Dimensions: 4 rows × 3 columns

| REF | NAME | TEXT |
| --- | --- | --- |
| 0x00 | REF_ALC_MIT | Referenzlauf Kurvenlicht mit Sensor |
| 0x01 | REF_ALC_OHNE | Referenzlauf Kurvenlicht ohne Sensor |
| 0x02 | REF_LWR | Referenzlauf LWR |
| 0xFF | ERROR | falscher Eingabewert |
