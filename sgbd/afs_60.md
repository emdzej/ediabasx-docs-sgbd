# afs_60.prg

- Jobs: [132](#jobs)
- Tables: [60](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | AFS |
| ORIGIN | BMW EE-21 Hans Sarnowski |
| REVISION | 8.02 |
| AUTHOR | S&S Joachim Schindlbeck |
| COMMENT | Aktive Front Steering fuer E60 |
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
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [IDENT_LESEN](#job-ident-lesen) - Identdaten KWP2000: $1A ReadECUIdentification SubID    $80 vordefinierte Tabellenstruktur auslesen Modus  : Default
- [IDENT_CUIFDT_LESEN](#job-ident-cuifdt-lesen) - CUIFDT aktuelles AIF Feld auslesen KWP2000: $1A ReadECUIdentification SubID    $86 CurrentUIFDataTable Modus  : Default
- [IDENT_PECUHN_LESEN](#job-ident-pecuhn-lesen) - Physikalische Hardware Nummer lesen, PECUHN KWP2000: $1A ReadECUIdentification SubID    $87 physicalECUHardwareNumber, PECUHN Modus  : Default
- [IDENT_SSECUSEN_LESEN](#job-ident-ssecusen-lesen) - Seriennummer aus EEPROM lesen KWP2000: $1A ReadECUIdentification SubID    $89 systemSupplierECUSerialNumber Modus  : Default
- [IDENT_SSS_LESEN](#job-ident-sss-lesen) - Revisionsnummer des MPC555 KWP2000: $1A ReadECUIdentification SubID    $8A systemSupplierSpecific Modus  : Default
- [IDENT_VIN_LESEN](#job-ident-vin-lesen) - Fahrgestellnummer KWP2000: $1A ReadECUIdentification SubID    $90 VIN VehicleIndentificationNumber Modus  : Default
- [IDENT_VMECUHN_LESEN](#job-ident-vmecuhn-lesen) - SG Herstelldatum KWP2000: $1A ReadECUIdentification SubID    $91 vehicleManufacturerECUHardwareNumber Modus  : Default
- [IDENT_SSECUHN_LESEN](#job-ident-ssecuhn-lesen) - KFZ-Typ auslesen (3 Byte) Datensatz-Typ auslesen (4 Byte) KWP2000: $1A ReadECUIdentification SubID    $92 systemSupplierECUHardwareNumber Modus  : Default
- [IDENT_SSECUHVN_LESEN](#job-ident-ssecuhvn-lesen) - KWP2000: $1A ReadECUIdentification SubID    $93 systemSupplierECUHardwareVersionNumber Modus  : Default
- [IDENT_SSECUSON_LESEN](#job-ident-ssecuson-lesen) - Uhrzeit der SG-Softwareprogrammerstellung Rechnername auf dem die Software (LowLevel) erzeugt wurde KWP2000: $1A ReadECUIdentification SubID    $94 systemSupplierECUSoftwareNumber Modus  : Default
- [IDENT_SSECUSVN_LESEN](#job-ident-ssecusvn-lesen) - interne Softwareversionsnummern des MPC und NEC abgelegt in ZF-LS Code KWP2000: $1A ReadECUIdentification SubID    $95 systemSupplierECUSoftwareVersionNumber Modus  : Default
- [IDENT_EROTAN_LESEN](#job-ident-erotan-lesen) - BehoerdenNummer KWP2000: $1A ReadECUIdentification SubID    $96 exhaustRegulationOrTypeApprovalNumber Modus  : Default
- [IDENT_SNOET_LESEN](#job-ident-snoet-lesen) - Variantenindex KWP2000: $1A ReadECUIdentification SubID    $97 systemNameOrEngineType
- [IDENT_RSCATSN_LESEN](#job-ident-rscatsn-lesen) - Testernummer KWP2000: $1A ReadECUIdentification SubID    $98 repairShopCodeandTesterSerialNumber Modus  : Default
- [IDENT_PD_LESEN](#job-ident-pd-lesen) - letztes Programmierdatum lesen KWP2000: $1A ReadECUIdentification SubID    $99 ProgrammingDate Modus  : Default
- [IDENT_VMECUHVN_LESEN](#job-ident-vmecuhvn-lesen) - HardwareNummer aus EEPROM lesen KWP2000: $1A ReadECUIdentification SubID    $9A vehicleManufacturerECUHardwareVersionNumber Modus  : Default
- [IDENT_VMCI_LESEN](#job-ident-vmci-lesen) - Codierindex lesen KWP2000: $1A ReadECUIdentification SubID    $9B vehicleManufacturerCodingIndex Modus  : Default
- [IDENT_VMDI_LESEN](#job-ident-vmdi-lesen) - Diagnoseindex lesen KWP2000: $1A ReadECUIdentification SubID    $9C vehicleManufacturerDiagnosticIndex Modus  : Default
- [IDENT_DOECUM_LESEN](#job-ident-doecum-lesen) - Herstelldatum des SG aus EEPROM lesen KWP2000: $1A ReadECUIdentification SubID    $9D dateOfECUManufacturing Modus  : Default
- [IDENT_SSI_LESEN](#job-ident-ssi-lesen) - Lieferantennummer/Index lesen KWP2000: $1A ReadECUIdentification SubID    $9E systemSupplierIndex Modus  : Default
- [IDENT_VMECUSLVN_LESEN](#job-ident-vmecuslvn-lesen) - MCV,OSV,FSV,RES Nummern lesen KWP2000: $1A ReadECUIdentification SubID    $9F vehicleManufECUSoftwareLayerVersionNumber Modus  : Default
- [HARDWARE_REFERENZ_LESEN_PAF_DAF](#job-hardware-referenz-lesen-paf-daf) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier SubID    $2502 HardwareReferenz 7 Byte ASCII 3 fach Ablage im Flash Bootblock Modus  : Default
- [PROGRAMM_REFERENZ_LESEN_PAF_DAF](#job-programm-referenz-lesen-paf-daf) - Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier SubID    $2503 ProgrammReferenz Modus  : Default
- [DATEN_REFERENZ_LESEN_PAF_DAF](#job-daten-referenz-lesen-paf-daf) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier SubID    $2504 DatenReferenz Modus  : Default
- [AFS_FLASH_ZEITEN_LESEN](#job-afs-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier SubID    $2501 Zeiten Modus  : Default
- [AFS_FLASH_BLOCKLAENGE_LESEN](#job-afs-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier SubID    $2506 MaximaleBlockLaenge Modus  : Default
- [AFS_ZIF_BACKUP_LESEN](#job-afs-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier SubID    $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification SubID    $80 ECUIdentificationDataTable Modus  : Default
- [AFS_AIF_LESEN](#job-afs-aif-lesen) - AIF/UIF Datenblock auslesen KWP2000: $23   ReadMemoryByAddress $AdrHigh AdrMid AdrLow UIFM UIFBlockLaenge SubID    $00      00     00     07   40 Modus  : Default
- [STATUS_VERSORGUNGEN](#job-status-versorgungen) - Auslesen der aktuellen Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier SubID    $01 InputOutputLocalIdentifier(IOLI) SubID    $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_AFS_OS](#job-status-afs-os) - Auslesen verschiedener Betriebssystem (OS,SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID    $02 InputOutputLocalIdentifier(IOLI) SubID    $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SICHERHEIT](#job-status-sicherheit) - Auslesen interner DPRAM Zustaende KWP2000: $30 InputOutputControlByLocalIdentifier $03 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PHASENSTROEME](#job-status-phasenstroeme) - Auslesen der Staenderstroeme I1 - I3 KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP)
- [STATUS_TEMPERATUREN](#job-status-temperaturen) - Auslesen der Motor und Endstufentemperaturen KWP2000: $30 InputOutputControlByLocalIdentifier $05 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_REDUNLWS_WINKELWERTE_ROH](#job-status-redunlws-winkelwerte-roh) - Auslesen des redundanten Fahrerlenkwinkels, gesendet von SZL uebertragen ueber serielle SN KWP2000: $30 InputOutputControlByLocalIdentifier $06 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_LWG_WINKELWERTE_PHYSIKALISCH](#job-status-lwg-winkelwerte-physikalisch) - Auslesen der Rohwerte vom Summenlenkwinkelsensor (singleturn Wert) ueber Botschaft (C3) LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN oder auch FW-CAN Wertebereich -90 &lt;--&gt; +90 Grad KWP2000: $30 InputOutputControlByLocalIdentifier $07 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_LWG_WINKELWERTE_ABSOLUT](#job-status-lwg-winkelwerte-absolut) - Auslesen des Summenlenkwinkels (multiturn) der von ASCET berechnet wurde Wert wird ueber FW-CAN vom AFS versendet ueber Botschaft (118) LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN oder auch FW-CAN KWP2000: $30 InputOutputControlByLocalIdentifier $08 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MOTORLAGEWINKEL](#job-status-motorlagewinkel) - Auslesen der Spannungen am Motor, und Motorlagewinkel Absolutwert(Istwert) KWP2000: $30 InputOutputControlByLocalIdentifier $09 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_FAHRERLENKWINKEL](#job-status-fahrerlenkwinkel) - Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0A InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_GESCHWINDIGKEITEN](#job-status-geschwindigkeiten) - Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0B InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_QUERBESCHLEUNIGUNG](#job-status-querbeschleunigung) - Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0C InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_GIERRATEN](#job-status-gierraten) - Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0D InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_DSC_INFO](#job-status-dsc-info) - Auslesen des DSC Status KWP2000: $30 InputOutputControlByLocalIdentifier $0E InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_WINKELWERTE](#job-status-winkelwerte) - Auslesen verschiedener Winkelwerte, wie Fahrerlenkwinkel,Summenlenkwinkel,Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier $0F InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PHASENSPANNUNGEN](#job-status-phasenspannungen) - Auslesen der Phasenspannungen U1 - U3 KWP2000: $30 InputOutputControlByLocalIdentifier $10 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP)
- [STATUS_QUALIFIER](#job-status-qualifier) - Auslesen verschiedener ASCET Qualifier KWP2000: $30 InputOutputControlByLocalIdentifier $11 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP)
- [STATUS_KLEMMEN_INFO](#job-status-klemmen-info) - Auslesen verschiedener Klemmenstati KWP2000: $30 InputOutputControlByLocalIdentifier $12 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ALIVE_INFO](#job-status-alive-info) - Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier $13InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_AFS](#job-status-afs) - Auslesen verschiedener SG Stati KWP2000: $30 InputOutputControlByLocalIdentifier $14 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_CAN_FEHLER_SIGNALE](#job-status-can-fehler-signale) - Auslesen verschiedener CAN Signalfehlerzustaende KWP2000: $30 InputOutputControlByLocalIdentifier $15 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PTCAN_SIGNALE](#job-status-ptcan-signale) - Auslesen verschiedener PT-CAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier $16 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_DYNAMIK](#job-status-dynamik) - Auslesen verschiedener PT-CAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier $17 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MPC_ERROR_INFO](#job-status-mpc-error-info) - Auslesen des MPC555 Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $30 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_NEC_ERROR_INFO](#job-status-nec-error-info) - Auslesen des NEC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $31 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MOTORLAGEWINKEL_OFFSET_LESEN](#job-status-motorlagewinkel-offset-lesen) - Auslesen des Motorlagewinkeloffsets KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 Anzahl der auszulesenden Bytes: 6 Speicher Adresse: 0x019E Modus  : Default
- [STEUERN_MOTORLAGEWINKEL_OFFSET_SCHREIBEN](#job-steuern-motorlagewinkel-offset-schreiben) - Schreiben des Motorlagewinkeloffsets an eine feste Adresse im EEProm KWP2000: $3D WriteMemoryByAddress,(WMBA) MemoryTypeIdentifier,ROMX = 2 Anzahl der zu schreibenden Bytes: 6 Speicher Adresse: 0x019E Modus  : Default
- [COD_C_LESEN](#job-cod-c-lesen) - Codierdaten lesen ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_C_SCHREIBEN](#job-cod-c-schreiben) - Codierdaten schreiben ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_N_LESEN](#job-cod-n-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_N_SCHREIBEN](#job-cod-n-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_PARAMETER_LESEN](#job-cod-parameter-lesen) - Codierdaten lesen ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet, Block 3000 Modus  : Default
- [FS_MPC_LOESCHEN](#job-fs-mpc-loeschen) - NUR Fehlerspeicher des MPC loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : $FF $00
- [FS_NEC_LOESCHEN](#job-fs-nec-loeschen) - NUR Fehlerspeicher des NEC loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : $FF $01
- [START_LWG_INIT](#job-start-lwg-init) - Start der Summenlenkwinkelinitialisierung KWP2000: $31 StartRoutineByLocalIdentifier Modus  : $50
- [START_EEPROM_INIT_MPC](#job-start-eeprom-init-mpc) - MPC EEPROM initialisieren KWP2000: $31 StartRoutineByLocalIdentifier Modus  : $51 RoutineLocalIdentifer
- [START_LWM_RUECKSETZEN](#job-start-lwm-ruecksetzen) - 1 Telegramm Motorlagewinkels auf ungueltig setzen, durch SG RESET 2 Telegramm Status des Motorlagewinkels wird ausgelesen KWP2000: $31 RequestRoutineResultsByLocalIdentifier $54 Inbetriebnahme Resultat abfragen Modus  : Default
- [LWM_INIT_ABFRAGEN](#job-lwm-init-abfragen) - Gueltigkeit des Rotorlagewinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $50 Inbetriebnahme Resultat abfragen Modus  : Default
- [LWG_INIT_ABFRAGEN](#job-lwg-init-abfragen) - Gueltigkeit des Summenlenkwinkels auslesen Quadrantenbestimmung KWP2000: $33 RequestRoutineResultsByLocalIdentifier $51 Inbetriebnahme Resultat abfragen Modus  : Default
- [NEC_FLASH_PROGRAMMIER_STATUS_LESEN](#job-nec-flash-programmier-status-lesen) - Zustand des NEC beim bzw. nach dem Flashen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $52 Inbetriebnahme Resultat abfragen Modus  : Default
- [NEC_EEPROM_LESEN](#job-nec-eeprom-lesen) - NEC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0000-0x01FF NEC Speichergroesse 512 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [NEC_EEPROM_SCHREIBEN](#job-nec-eeprom-schreiben) - NEC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $3D writeMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0000-0x01FF NEC Speichergroesse 512 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [MPC_EEPROM_LESEN](#job-mpc-eeprom-lesen) - MPC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0200-0x0FFF NEC Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [MPC_EEPROM_SCHREIBEN](#job-mpc-eeprom-schreiben) - MPC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $3D writeMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige MPC Speicher Adressen: 0x0200-0x0FFF MPC Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [ZF_FACTORY_DATEN_LESEN](#job-zf-factory-daten-lesen) - MPC EEPROM Daten lesen fuer INPA Darstellung KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige MPC Speicher Adressen: 0x0200-0x0FFF EEPROM Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [STEUERN_DVR_TESTSTIM](#job-steuern-dvr-teststim) - Teststimuli fuer diversitaeres Rechnen setzen KWP2000: $3B WriteDataByLocalIdentifier setzt Testvektoren fuers diversi. Rechnen 2 Argumente 2,5678
- [STEUERN_DPRAM_TESTSTIM](#job-steuern-dpram-teststim) - Teststimuli DX Mechanismus setzen Erweitertes KWP2000 setzen, fuer DEBUG Zwecke KWP2000: $3B WriteDataByLocalIdentifier 2 Argumente 0,2

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

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident-lesen"></a>
### IDENT_LESEN

Identdaten KWP2000: $1A ReadECUIdentification SubID    $80 vordefinierte Tabellenstruktur auslesen Modus  : Default

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
| ID_VAR_INDEX_Z | string | Varianten-Index |
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
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-cuifdt-lesen"></a>
### IDENT_CUIFDT_LESEN

CUIFDT aktuelles AIF Feld auslesen KWP2000: $1A ReadECUIdentification SubID    $86 CurrentUIFDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BELEGT | int | 0 --&gt; gesmmtes AIF Feld ist nich frei, 1--&gt; mindestens ein Byte enthaelt einen Wert ungleich 0xFF |
| AIF_ANZ_DATEN_HEX | string | Telegrammwert in HEX Verweis auf naechstes AIF Feld |
| AIF_ANZ_DATEN | int | AIF Feld Typ Groesse des jeweiligen Eintrages ist aus dem Adressofset ersichtlich 0x40_hex ( 64_dez ) Power PC 0x33_hex ( 51_dez ) fuer alle anderen Anwender des grossen AIF Feldes 0x12_hex ( 18_dez ) letztmoeglicher Blockeintrag 0xFE_hex ( 254_dez ) letztmoeglicher Eintrag 0x01_hex ( 64_dez ) nur ein Eintrag der aber ueberschreibbar ist 0xFF_hex ( 255_dez ) freier Speicherplatz 0x00_hex ( 00_dez ) freier Speicherplatz |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FAHRGESTELL_NR_HEX | string | Telegrammdarstellung Fahrgestellnummer (7 Byte) |
| AIF_PROGRAMMIER_DATUM | string | Programmierdatum in yyyy.mm.tt |
| AIF_PROGRAMMIER_DATUM_HEX | string | Speicherdarstellung/Telegrammdarstellung (4 Byte) |
| AIF_ZUSAMMENBAU_NR | string | Zusammenbaunummer |
| AIF_ZUSAMMENBAU_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_DATENSATZ_NR | string | Datensatznummer |
| AIF_DATENSATZ_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_DATENSATZ_NR_UHRZEIT | string | Uhrzeit der Codeerzeugung als Teil in der Datensatznummer abgelegt Gesamtlaenge 6 Byte, Teilestringlaenge fuer die Uhrzeit die letzten 2 Byte [hh:mm] |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_BEHOERDEN_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_HAENDLER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (3 Byte) |
| AIF_TESTER_NR | string | Haendlernummer |
| AIF_TESTER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (5 Byte) |
| AIF_RECHNER_NAME | string | Rechnername auf dem die Software erzeugt wurde |
| AIF_RECHNER_NAME_HEX | string | Rechnername auf dem die Software erzeugt wurde,Speicherdarstellung/Telegrammdarstellung (8 Byte) |
| AIF_KM_STAND | string | Kilometerstand bei der Programmierung |
| AIF_KM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (1 Byte) |
| AIF_PROGRAMM_STAND | string | Programmstand als Programmreferenz |
| AIF_PROGRAMM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (12 Byte) |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 10-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig |
| AIF_FG_NR_LANG_HEX | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig Speicherdarstellung/Telegrammdarstellung (10 Byte) |
| AIF_RESERVE | string | Reserve fuer MPC555 |
| AIF_RESERVE_HEX | string | Speicherdarstellung/Telegrammdarstellung (13 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-pecuhn-lesen"></a>
### IDENT_PECUHN_LESEN

Physikalische Hardware Nummer lesen, PECUHN KWP2000: $1A ReadECUIdentification SubID    $87 physicalECUHardwareNumber, PECUHN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HWNR_PHYS | string | physikalische Hardwarenummer |
| HWNR_PHYS_HEX | string | Telegrammdarstellung physikalische Hardwarenummer (6 Byte) nur einfach Darstellung |
| ID_HW_NR_1 | string | physikalische Hardwarenummer |
| ID_HW_NR_2 | string | physikalische Hardwarenummer |
| ID_HW_NR_3 | string | physikalische Hardwarenummer |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ssecusen-lesen"></a>
### IDENT_SSECUSEN_LESEN

Seriennummer aus EEPROM lesen KWP2000: $1A ReadECUIdentification SubID    $89 systemSupplierECUSerialNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERIENNUMMER | string | Seriennummer des Steuergeraets (9 Byte), aus EEPROM |
| SERIENNUMMER_HEX | string | Seriennummer des Steuergeraets |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-sss-lesen"></a>
### IDENT_SSS_LESEN

Revisionsnummer des MPC555 KWP2000: $1A ReadECUIdentification SubID    $8A systemSupplierSpecific Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MPC555_REVISIONS_NR | string | IMMR (Internal Memory Map Register) wird ausgelesen Prozessorrevisionsnummer MPC555 2-stellig in diesem RESULT werden nur 2 Byte ausgewertet |
| MPC555_REVISIONS_NR_HEX | string | Telegrammdarstellung MPC555 Revisionsnummer (4 Byte) |
| MPC555_REVISIONS_TEXT | string | Prozessorrevisionsnummer MPC555 2-stellig in diesem RESULT werden nur 2 Byte ausgewertet in Tabelle 'MPCRev' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vin-lesen"></a>
### IDENT_VIN_LESEN

Fahrgestellnummer KWP2000: $1A ReadECUIdentification SubID    $90 VIN VehicleIndentificationNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| FAHRGESTELL_NR_HEX | string | Telegrammdarstellung Fahrgestellnummer (7 Byte) |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vmecuhn-lesen"></a>
### IDENT_VMECUHN_LESEN

SG Herstelldatum KWP2000: $1A ReadECUIdentification SubID    $91 vehicleManufacturerECUHardwareNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR_1 | string | BMW TeileNummer HardwareSternNummer |
| ID_BMW_NR_1_HEX | string | BMW TeileNummer HardwareSternNummer Telegrammdarstellung |
| ID_BMW_NR_2 | string | BMW TeileNummer HardwareSternNummer |
| ID_BMW_NR_3 | string | BMW TeileNummer HardwareSternNummer |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ssecuhn-lesen"></a>
### IDENT_SSECUHN_LESEN

KFZ-Typ auslesen (3 Byte) Datensatz-Typ auslesen (4 Byte) KWP2000: $1A ReadECUIdentification SubID    $92 systemSupplierECUHardwareNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FZG_TYP | string | Fahrzeugart ( 3 Byte ) |
| FZG_TYP_HEX | string | Fahrzeugart ( 3 Byte ) in Telegrammdarstellung |
| INTEGRATIONS_STUFE | string | aktuelle Interationssufe z.B. 'I330'( 4 Byte ) |
| INTEGRATIONS_STUFE_HEX | string | aktuelle Interationssufe z.B. 'I330'( 4 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ssecuhvn-lesen"></a>
### IDENT_SSECUHVN_LESEN

KWP2000: $1A ReadECUIdentification SubID    $93 systemSupplierECUHardwareVersionNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ssecuson-lesen"></a>
### IDENT_SSECUSON_LESEN

Uhrzeit der SG-Softwareprogrammerstellung Rechnername auf dem die Software (LowLevel) erzeugt wurde KWP2000: $1A ReadECUIdentification SubID    $94 systemSupplierECUSoftwareNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| UHRZEIT | string | Uhrzeit [hh:mm] der Codeerzeugung ( 2 Byte ) |
| UHRZEIT_HEX | string | Uhrzeit der Codeerzeugung ( 2 Byte ) in Telegrammdarstellung |
| RECHNERNAME | string | Z.B: "WM193316"( 8 Byte ) |
| RECHNERNAME_HEX | string | Z.B: "WM193316"( 8 Byte )in Telegrammdarstellung |
| ASCET_DB_NAME | string | Z.B: "AFS_I520_S810"( Laenge maximal 30 Byte ) |
| ASCET_DB_NAME_HEX | string | Z.B: "AFS_I520_S810"( Laenge maximal 30 Byte )in Telegrammdarstellung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ssecusvn-lesen"></a>
### IDENT_SSECUSVN_LESEN

interne Softwareversionsnummern des MPC und NEC abgelegt in ZF-LS Code KWP2000: $1A ReadECUIdentification SubID    $95 systemSupplierECUSoftwareVersionNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MPC_SVN | string | aktuelle MPC Softwarenummer im ZF-LS Code( 11 Byte ) |
| NEC_SVN | string | aktuelle NEC Softwarenummer im ZF-LS Code( 11 Byte ) |
| NEC_RES | string | aktuelle NEC Softwarenummer in den Logistikdaten Code( 3 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-erotan-lesen"></a>
### IDENT_EROTAN_LESEN

BehoerdenNummer KWP2000: $1A ReadECUIdentification SubID    $96 exhaustRegulationOrTypeApprovalNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BEHOERDEN_NR | string | Behoerdennummer |
| BEHOERDEN_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-snoet-lesen"></a>
### IDENT_SNOET_LESEN

Variantenindex KWP2000: $1A ReadECUIdentification SubID    $97 systemNameOrEngineType

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_VAR_INDEX | int | Varianten-Index |
| ID_VAR_INDEX_Z | string | Varianten-Index |
| ID_VAR_INDEX_HEX | string | Speicherdarstellung/Telegrammdarstellung (2 Byte) |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-rscatsn-lesen"></a>
### IDENT_RSCATSN_LESEN

Testernummer KWP2000: $1A ReadECUIdentification SubID    $98 repairShopCodeandTesterSerialNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-pd-lesen"></a>
### IDENT_PD_LESEN

letztes Programmierdatum lesen KWP2000: $1A ReadECUIdentification SubID    $99 ProgrammingDate Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| ID_DATUM_SW | string | TT.MM.JJJJ |
| ID_DATUM_SW_HEX | string | Speicherdarstellung/Telegrammdarstellung (4 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vmecuhvn-lesen"></a>
### IDENT_VMECUHVN_LESEN

HardwareNummer aus EEPROM lesen KWP2000: $1A ReadECUIdentification SubID    $9A vehicleManufacturerECUHardwareVersionNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_HW_NR | string | BMW-Hardwarenummer, z.B. C2 |
| ID_HW_NR_HEX | string | BMW-Hardwarenummer/ Telegrammdarstellung |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vmci-lesen"></a>
### IDENT_VMCI_LESEN

Codierindex lesen KWP2000: $1A ReadECUIdentification SubID    $9B vehicleManufacturerCodingIndex Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_COD_INDEX | int | Codier-Index |
| ID_COD_INDEX_HEX | string | Codierindex/ Telegrammdarstellung 1 Byte |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vmdi-lesen"></a>
### IDENT_VMDI_LESEN

Diagnoseindex lesen KWP2000: $1A ReadECUIdentification SubID    $9C vehicleManufacturerDiagnosticIndex Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_DIAG_INDEX | int | Diagnoseindex, von TI beziehen |
| ID_DIAG_INDEX_HEX | string | Diagnoseindex/ Telegrammdarstellung 2 Byte |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-doecum-lesen"></a>
### IDENT_DOECUM_LESEN

Herstelldatum des SG aus EEPROM lesen KWP2000: $1A ReadECUIdentification SubID    $9D dateOfECUManufacturing Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SG_HERSTELL_DATUM | string | Programmierdatum in yyyy.mm.tt |
| ID_SG_HERSTELL_DATUM_HEX | string | Speicherdarstellung/Telegrammdarstellung (4 Byte) |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ssi-lesen"></a>
### IDENT_SSI_LESEN

Lieferantennummer/Index lesen KWP2000: $1A ReadECUIdentification SubID    $9E systemSupplierIndex Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_NR_HEX | string | Lieferanten-Nummer/ Telegrammdarstellung ( 1 Byte ) |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vmecuslvn-lesen"></a>
### IDENT_VMECUSLVN_LESEN

MCV,OSV,FSV,RES Nummern lesen KWP2000: $1A ReadECUIdentification SubID    $9F vehicleManufECUSoftwareLayerVersionNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_MCV_HEX | string | Softwarenummer (message catalogue version), Telegrammdarstellung ( 3 Byte ) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_FSV_HEX | string | Softwarenummer (functional software version), Telegrammdarstellung ( 3 Byte ) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_OSV_HEX | string | Softwarenummer (operating system version), Telegrammdarstellung ( 3 Byte ) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| ID_SW_NR_RES_HEX | string | Softwarenummer (reserved - currently unused), Telegrammdarstellung ( 3 Byte ) |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hardware-referenz-lesen-paf-daf"></a>
### HARDWARE_REFERENZ_LESEN_PAF_DAF

Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier SubID    $2502 HardwareReferenz 7 Byte ASCII 3 fach Ablage im Flash Bootblock Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HARDWARE_REFERENZ | string | Hardware Referenz ( 7 Byte ASCII ) |
| HARDWARE_REFERENZ_HEX | string | Hardware Referenz, Telegrammdarstellung ( 7 Byte ) |
| HARDWARE_ZZZ | string | Hardware Referenz XXX Nummer |
| HARDWARE_PPP | string | Hardware Referenz PPP Nummer |
| HARDWARE_X | string | Hardware Referenz X Nummer |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-programm-referenz-lesen-paf-daf"></a>
### PROGRAMM_REFERENZ_LESEN_PAF_DAF

Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier SubID    $2503 ProgrammReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROGRAMM_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex( 12 Byte ASCII 3-fach flash ) |
| PROGRAMM_REFERENZ_HEX | string | Herstellerkennung & Projektnummer & Projektindex( 12 Byte ASCII 3-fach flash ) |
| HARDWARE_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| HARDWARE_ZZZ | string | Hardware Referenz XXX Nummer |
| HARDWARE_PPP | string | Hardware Referenz PPP Nummer |
| HARDWARE_X | string | Hardware Referenz X Nummer |
| PROGRAMM_V | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_BB | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_X | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_H | string | Herstellerkennung & Projektnummer & Projektindex |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-daten-referenz-lesen-paf-daf"></a>
### DATEN_REFERENZ_LESEN_PAF_DAF

Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier SubID    $2504 DatenReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_REFERENZ | string | Daten Referenz |
| DATEN_REFERENZ_HEX | string | ( 17 Byte ASCII 3-fach flash ) |
| PROGRAMM_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| HARDWARE_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| HARDWARE_ZZZ | string | Hardware Referenz XXX Nummer |
| HARDWARE_PPP | string | Hardware Referenz PPP Nummer |
| HARDWARE_X | string | Hardware Referenz X Nummer |
| PROGRAMM_V | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_BB | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_X | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_H | string | Herstellerkennung & Projektnummer & Projektindex |
| DATEN_D | string | Daten Referenz |
| DATEN_XXXX | string | Daten Referenz |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-afs-flash-zeiten-lesen"></a>
### AFS_FLASH_ZEITEN_LESEN

Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier SubID    $2501 Zeiten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHZEIT | int | Flash Loeschzeit in Sekunden |
| FLASH_SIGNATURTESTZEIT | int | Flash Signaturtestzeit in Sekunden |
| FLASH_RESETZEIT | int | Flash Resetzeit in Sekunden |
| FLASH_AUTHENTISIERZEIT | int | Flash Authentisierberechnungszeit in Sekunden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-afs-flash-blocklaenge-lesen"></a>
### AFS_FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier SubID    $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_GESAMT | int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-afs-zif-backup-lesen"></a>
### AFS_ZIF_BACKUP_LESEN

Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier SubID    $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification SubID    $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZIF_BACKUP_PROGRAMM_REFERENZ | string | PRGREFB ProgrammReferenzBackup letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter aenderungsindex h     : Programmstandersteller |
| ZIF_BACKUP_SG_KENNUNG | string | ZZZ |
| ZIF_BACKUP_PROJEKT | string | PPPxV |
| ZIF_BACKUP_PROGRAMM_STAND | string | BBxh |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BACKUP_BMW_HW | string | VMECUH*NB vehicleManufECUHW*NumberBackup BMW Hardware* Nummer |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_DATEN_2 | binary | Hex-Auftrag an SG |

<a id="job-afs-aif-lesen"></a>
### AFS_AIF_LESEN

AIF/UIF Datenblock auslesen KWP2000: $23   ReadMemoryByAddress $AdrHigh AdrMid AdrLow UIFM UIFBlockLaenge SubID    $00      00     00     07   40 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NR | int | == 0 : aktuelles AIF &gt; 0 : Nummer des zu lesenden AIF default = 0 : aktuelles AIF AIF Blocknummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ANZ_DATEN_HEX | string | Telegrammwert in HEX Verweis auf naechstes AIF Feld |
| AIF_ANZ_DATEN | int | AIF Feld Typ Groesse des jeweiligen Eintrages ist aus dem Adressofset ersichtlich 0x40_hex ( 64_dez ) Power PC 0x33_hex ( 51_dez ) fuer alle anderen Anwender des grossen AIF Feldes 0x12_hex ( 18_dez ) letztmoeglicher Blockeintrag 0xFE_hex ( 254_dez ) letztmoeglicher Eintrag 0x01_hex ( 64_dez ) nur ein Eintrag der aber ueberschreibbar ist 0xFF_hex ( 255_dez ) freier Speicherplatz 0x00_hex ( 00_dez ) freier Speicherplatz |
| BELEGT | int | 0 --&gt; gesmmtes AIF Feld ist nich frei, 1--&gt; mindestens ein Byte enthaelt einen Wert ungleich 0xFF |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ADRESSE | long | logische Adresse des AIF Feldes |
| AIF_ADRESSE_PHYSIKALISCH | long | physikalische Adresse des AIF Feldes |
| LOGISCHE_ADRESSE | string | Telegrammwert in HEX logische Adresse des AIF Feldes |
| PHYSIKALISCHE_ADRESSE | string | Telegrammwert in HEX physikalische Adresse des AIF Feldes |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FAHRGESTELL_NR_HEX | string | Telegrammdarstellung Fahrgestellnummer (7 Byte) |
| AIF_PROGRAMMIER_DATUM | string | Programmierdatum in yyyy.mm.tt |
| AIF_PROGRAMMIER_DATUM_HEX | string | Speicherdarstellung/Telegrammdarstellung (4 Byte) |
| AIF_ZUSAMMENBAU_NR | string | Zusammenbaunummer |
| AIF_ZUSAMMENBAU_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_DATENSATZ_NR | string | Datensatznummer (6 Byte) |
| AIF_DATENSATZ_NR_UHRZEIT | string | Uhrzeit der Codeerzeugung als Teil in der Datensatznummer abgelegt Gesamtlaenge 6 Byte, Teilestringlaenge fuer die Uhrzeit die letzten 2 Byte [hh:mm] |
| AIF_DATENSATZ_ISTUFE | string | Nummer der Integrationstufe als der Bootblock erzeugt wurde Gesamtlaenge 6 Byte, Teilestringlaenge fuer die IStufe 4 Byte [I331] |
| AIF_DATENSATZ_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_BEHOERDEN_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_HAENDLER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (3 Byte) |
| AIF_TESTER_NR | string | Haendlernummer |
| AIF_TESTER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (5 Byte) |
| AIF_RECHNER_NAME | string | Rechnername auf dem die Software erzeugt wurde |
| AIF_RECHNER_NAME_HEX | string | Rechnername auf dem die Software erzeugt wurde,Speicherdarstellung/Telegrammdarstellung (8 Byte) |
| AIF_KM_STAND | string | Kilometerstand bei der Programmierung |
| AIF_KM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (1 Byte) |
| AIF_PROGRAMM_STAND | string | Programmstand als Programmreferenz |
| AIF_PROGRAMM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (12 Byte) |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 10-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig |
| AIF_FG_NR_LANG_HEX | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig Speicherdarstellung/Telegrammdarstellung (10 Byte) |
| AIF_RESERVE | string | Reserve fuer MPC555 |
| AIF_RESERVE_HEX | string | Speicherdarstellung/Telegrammdarstellung (13 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-status-versorgungen"></a>
### STATUS_VERSORGUNGEN

Auslesen der aktuellen Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier SubID    $01 InputOutputLocalIdentifier(IOLI) SubID    $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME30_WERT | real | Spannung an Klemme 30 Bereich: 0 bis 20V |
| STAT_KLEMME30_EINH | string | Volt |
| STAT_VERSORGUNG_SENSOREN_5V_WERT | real | Versorgung der 5V Sensoren Bereich:0 bis 5V |
| STAT_VERSORGUNG_SENSOREN_5V_EINH | string | Volt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-afs-os"></a>
### STATUS_AFS_OS

Auslesen verschiedener Betriebssystem (OS,SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID    $02 InputOutputLocalIdentifier(IOLI) SubID    $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEM_MPC555_AKTUELL | int | aktueller Systemstatus des MPC gueltige Werte 0 bis 6 POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 |
| STAT_SYSTEM_MPC555_AKTUELL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_NEC_AKTUELL | int | aktueller Systemstatus des NEC gueltige Werte 0 bis 6 POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 |
| STAT_SYSTEM_NEC_AKTUELL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_MPC555_DESIRE | int | gewuenschter Status des MPC gueltige Werte 0 bis ? |
| STAT_SYSTEM_MPC555_DESIRE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_NEC_DESIRE | int | gewuenschter Status des NEC gueltige Werte 0 bis ? |
| STAT_SYSTEM_NEC_DESIRE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_CURRENT_OP_MODE | int | OP Status von ERCOSEK gueltige Werte 1 bis 4 |
| STAT_CURRENT_OP_MODE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; CurrentOPModeStati |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-sicherheit"></a>
### STATUS_SICHERHEIT

Auslesen interner DPRAM Zustaende KWP2000: $30 InputOutputControlByLocalIdentifier $03 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DPRAM_ZUSTAND | int | Sicherheitszustand des DPRAMs gueltige Werte 0 bis 2 |
| STAT_DPRAM_ZUSTAND_TEXT | string | Textausgabe ueber Tabellenzugriff (DPRAMStati) |
| STAT_DPRAM_READ_STATE | int | Sicherheitszustand des DPRAMs gueltige Werte 0 bis 2 |
| STAT_DPRAM_BIT_INTERRUPT | int | Sicherheitszustand des DPRAMs gueltige Werte 0 bis 2 |
| STAT_ROM_CHECK_SECTOR | int | wird nur hochgezaehlt wenn das SG im NORMANL Mode ist es werden 361 Sectoren der Software ueberprueft gueltige Werte 1 bis 361 |
| STAT_ROM_CHECK_SECTOR_MAX | int | Anzahl der durch den ROM Check zu pruefenden Sektoren gueltiger Wert 361 |
| STAT_ROM_CHECK_AKTUELLE_SECTOR_STARTADRESSE_HEX | string | Zugriff auf ZF-LS ROM-Check Adresstabelle aktuelle gepruefter ROMcheck Sektor z.B. 57 mit Startadresse 0x0003FF18 |
| STAT_ROM_CHECK_AKTUELLE_SECTOR_ENDEADRESSE_HEX | string | Zugriff auf ZF-LS ROM-Check Adresstabelle aktuelle gepruefter ROMcheck Sektor z.B. 57 mit Endadresse 0x00040F16 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-phasenstroeme"></a>
### STATUS_PHASENSTROEME

Auslesen der Staenderstroeme I1 - I3 KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHASENSTROM_I1_WERT | real | Strom am Steller ( 2 Byte ) Einheit[A] |
| STAT_PHASENSTROM_I2_WERT | real | Strom am Steller ( 2 Byte ) Einheit[A] |
| STAT_PHASENSTROM_I3_WERT | real | Strom am Steller ( 2 Byte ) Einheit[A] |
| STAT_PHASENSTROM_EINH | string | Einheit [Ampere] A |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-temperaturen"></a>
### STATUS_TEMPERATUREN

Auslesen der Motor und Endstufentemperaturen KWP2000: $30 InputOutputControlByLocalIdentifier $05 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTOR_TEMPERATUR_MPC555_WERT | real | vorzeichenbehafteter Temp.Wert des Stellmotors ( 1 Byte ) gueltiger Temperaturbereich -70 °C .... + 185 °C |
| STAT_MOTOR_TEMPERATUR_NEC_WERT | real | vorzeichenbehafteter Temp.Wert des Stellmotors ( 1 Byte ) gueltiger Temperaturbereich -70 °C .... + 185 °C |
| STAT_ENDSTUFE_TEMPERATUR_MPC555_WERT | real | vorzeichenbehafteter Temp.Wert der Endstufe auf der Platine gemessen , 1 Byte gueltiger Temperaturbereich -70 °C .... + 185 °C |
| STAT_ENDSTUFE_TEMPERATUR_NEC_WERT | real | vorzeichenbehafteter Temp.Wert der Endstufe auf der Platine gemessen 1 Byte gueltiger Temperaturbereich -70 °C .... + 185 °C |
| STAT_OEL_TEMPERATUR_MPC555_WERT | real | vorzeichenbehafteter Temp.Wert fuer die Hydraulikoeltemperatur , 1 Byte gueltiger Temperaturbereich -70 °C .... + 185 °C |
| STAT_TEMPERATUR_EINH | string | Einheit [Grad Celcius] Grad °C |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-redunlws-winkelwerte-roh"></a>
### STATUS_REDUNLWS_WINKELWERTE_ROH

Auslesen des redundanten Fahrerlenkwinkels, gesendet von SZL uebertragen ueber serielle SN KWP2000: $30 InputOutputControlByLocalIdentifier $06 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRER_LENKWINKEL_S1_ROH_WERT | int | Telegrammwert ( 1 Byte )  |
| STAT_FAHRER_LENKWINKEL_S1_ROH_VOLT | real | errechneter Spannungswert in Volt ( 1 Byte ) Skalierung 0,1 Volt, Quantisierung 5 Volt/ 8bit, 1 bit --&gt; 0,01961 Volt |
| STAT_FAHRER_LENKWINKEL_S2_ROH_WERT | int | Telegrammwert ( 1 Byte )  |
| STAT_FAHRER_LENKWINKEL_S2_ROH_VOLT | real | errechneter Spannungswert in Volt ( 1 Byte ) Skalierung 0,1 Volt, Quantisierung 5 Volt/ 8bit, 1 bit --&gt; 0,01961 Volt |
| STAT_FAHRER_LENKWINKEL_POTIREF_ROH_WERT | int | Telegrammwert ( 1 Byte )  |
| STAT_FAHRER_LENKWINKEL_POTIREF_ROH_VOLT | real | errechneter Spannungswert in Volt ( 1 Byte ) Skalierung 0,1 Volt, Quantisierung 5 Volt/ 8bit, 1 bit --&gt; 0,01961 Volt |
| STAT_FAHRER_LENKWINKEL_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des Fahrerlenkwinkels vom SZL (0..15) |
| STAT_VOLT_EINH | string | Volt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-lwg-winkelwerte-physikalisch"></a>
### STATUS_LWG_WINKELWERTE_PHYSIKALISCH

Auslesen der Rohwerte vom Summenlenkwinkelsensor (singleturn Wert) ueber Botschaft (C3) LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN oder auch FW-CAN Wertebereich -90 &lt;--&gt; +90 Grad KWP2000: $30 InputOutputControlByLocalIdentifier $07 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SUMMENLENKWINKEL_WERT | real | LO-CAN (FahrwerkCAN) Rohwert des Summenlenkwinkels ( 2 Byte ) vom Summenlenkwinkelsensor, Botschaft (C3) Einheit[Grad] |
| STAT_SUMMENLENKWINKEL_EINH | string | Einheit [Winkelgrad] Grad |
| STAT_SUMMENLENKWINKEL_CAN_ERROR_WERT | int | Status Summenlenkwinkel ( 1 Byte ) moegliche Faelle 0 --&gt; i.o 2 --&gt; init 4 --&gt; timeout 8 --&gt; plausibel |
| STAT_SUMMENLENKWINKEL_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-lwg-winkelwerte-absolut"></a>
### STATUS_LWG_WINKELWERTE_ABSOLUT

Auslesen des Summenlenkwinkels (multiturn) der von ASCET berechnet wurde Wert wird ueber FW-CAN vom AFS versendet ueber Botschaft (118) LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN oder auch FW-CAN KWP2000: $30 InputOutputControlByLocalIdentifier $08 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SUMMENLENKWINKEL_ABSOLUT_WERT | real | FW-CAN (Fahrwerk CAN) Wert des multiturn Summenlenkwinkels ( 2 Byte ) vorzeichnenbehafteter Wert, Skalierung (180/4096, Wertebereich bis ca +-1500 Grad) von ASCET berechnet Einheit[Grad] |
| STAT_SUMMENLENKWINKEL_ABSOLUT_EINH | string | Einheit [Winkelgrad] Grad |
| STAT_SUMMENLENKWINKEL_GESCHWINDIGKEIT_ABSOLUT_WERT | real | FW-CAN (Fahrwerk CAN) Wert der absoluten Summenlenkwinkelgeschwindigkeit( 2 Byte ) vorzeichnenbehafteter Wert, Skalierung (???) von ASCET berechnet Einheit[Grad/s] |
| STAT_SUMMENLENKWINKEL_GESCHWINDIGKEIT_ABSOLUT_EINH | string | Einheit [grad/s] Grad/s |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-motorlagewinkel"></a>
### STATUS_MOTORLAGEWINKEL

Auslesen der Spannungen am Motor, und Motorlagewinkel Absolutwert(Istwert) KWP2000: $30 InputOutputControlByLocalIdentifier $09 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORLAGEWINKEL_SIN_VOLT | real | errechneter Spannungswert in Volt ( 2 Byte ) Skalierung 1000 Volt, Quantisierung 5 Volt/ 10bit, 1 bit --&gt; 0,004888 Volt |
| STAT_MOTORLAGEWINKEL_COS_VOLT | real | errechneter Spannungswert in Volt ( 2 Byte ) Skalierung 1000 Volt, Quantisierung 5 Volt/ 10bit, 1 bit --&gt; 0,004888 Volt |
| STAT_MOTORLAGEWINKEL_EINH | string | Volt |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom MPC ( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC_EINH | string | Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom NEC( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC_EINH | string | Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT | real | Motorlagewinkel Absoultwert in Grad eingelesen von ASCET( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT_EINH | string | Grad |
| STAT_ABWEICHUNG_MOTORWINKEL_WERT | real | Abweichung Motorwinkel von ASCET Var. MSG_R_LwDMdiffabs_filt ( 4 Byte ) Skalierung 1 |
| STAT_ABWEICHUNG_MOTORWINKEL_EINH | string | Grad Fahrerwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-fahrerlenkwinkel"></a>
### STATUS_FAHRERLENKWINKEL

Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0A InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber PT-CAN Laenge: ( 2 Byte ) Wertebereich[+-500] |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit [Grad] |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; in Ordnung, SZL initialisiert ) moegliche Zustaende ( 1 --&gt; SZL muss noch aufgesetzt werden, Initialisierung noch durchzufuehren ) moegliche Zustaende ( 2 --&gt; nicht definiert ) Gueltigkeit des Fahrerlenkwinkels vom SZL gueltig/ungueltig, ( 1 Byte ) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; GueLwD  ( 1 Byte ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber PT-CAN Laenge: ( 2 Byte ) CAN-ID  : 196 / 0x0C4 Wertebereich[-1440Grad/s...1440Grad/s] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit [Grad/s] |
| STAT_LENKRADWINKELSCHIEFSTAND_WERT | real | Lenkradwinkelschiefstand von ASCET Var. MSG_R_DiffLwGLwvirt ( 4 Byte ) Rohwert in rad |
| STAT_LENKRADWINKELSCHIEFSTAND_EINH | string | Grad Fahrerwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-geschwindigkeiten"></a>
### STATUS_GESCHWINDIGKEITEN

Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0B InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RAD_GESCHWINDIGKEIT_VL_WERT | real | Radgeschwinigkeit vorne links ueber LO-CAN Laenge: ( 2 Byte ) Wertebereich[+300 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_VL_EINH | string | Einheit [km/h] |
| STAT_RAD_GESCHWINDIGKEIT_VR_WERT | real | Radgeschwinigkeit vorne rechts ueber LO-CAN Laenge: ( 2 Byte ) Wertebereich[+300 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_VR_EINH | string | Einheit [km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HL_WERT | real | Radgeschwinigkeit hinten links ueber LO-CAN Laenge: ( 2 Byte ) Wertebereich[+300 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HL_EINH | string | Einheit [km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HR_WERT | real | Radgeschwinigkeit hinten rechts ueber LO-CAN Laenge: ( 2 Byte ) Wertebereich[+300 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HR_EINH | string | Einheit [km/h] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber PT-CAN Laenge: ( 2 Byte ) CAN-ID  : 196 / 0x0C4 Wertebereich[-1440Grad/s...1440Grad/s] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit [Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_1_WERT | real | Giergeschwinigkeit 1 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 112 / 0x070 Wertebereich[] |
| STAT_GIERGESCHWINDIGKEIT_1_EINH | string | Einheit [Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_2_WERT | real | Giergeschwinigkeit 2 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 203 / 0x0CB Wertebereich[] |
| STAT_GIERGESCHWINDIGKEIT_2_EINH | string | Einheit [Grad/s] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-querbeschleunigung"></a>
### STATUS_QUERBESCHLEUNIGUNG

Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0C InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QUERBESCHLEUNIGUNG_1_WERT | real | Querbeschl. 1 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 112 / 0x070 Wertebereich[] |
| STAT_QUERBESCHLEUNIGUNG_1_EINH | string | Einheit [m/s*s] |
| STAT_QUERBESCHLEUNIGUNG_1_G_WERT | real | Querbeschl. 1 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 112 / 0x070 normiert auf 9.81 |
| STAT_QUERBESCHLEUNIGUNG_1_G_EINH | string | Einheit [g] |
| STAT_QUERBESCHLEUNIGUNG_2_WERT | real | Querbeschl. 2 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 203 / 0x0CB Wertebereich[] |
| STAT_QUERBESCHLEUNIGUNG_2_EINH | string | Einheit [m/s*s] |
| STAT_QUERBESCHLEUNIGUNG_2_G_WERT | real | Querbeschl. 1 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 112 / 0x070 normiert auf 9.81 |
| STAT_QUERBESCHLEUNIGUNG_2_G_EINH | string | Einheit [g] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-gierraten"></a>
### STATUS_GIERRATEN

Auslesen des Fahrerlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier $0D InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GIERGESCHWINDIGKEIT_1_WERT | real | Giergeschwinigkeit 1 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 112 / 0x070 Wertebereich[] |
| STAT_GIERGESCHWINDIGKEIT_1_EINH | string | Einheit [Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_2_WERT | real | Giergeschwinigkeit 2 ueber LO-CAN Laenge: ( 2 Byte ) CAN-ID : 203 / 0x0CB Wertebereich[] |
| STAT_GIERGESCHWINDIGKEIT_2_EINH | string | Einheit [Grad/s] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-dsc-info"></a>
### STATUS_DSC_INFO

Auslesen des DSC Status KWP2000: $30 InputOutputControlByLocalIdentifier $0E InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DSC_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des DSC (0..14) |
| STAT_GUELTIGKEIT_DSC_WERT | int | moegliche Zustaende ( 0 --&gt; in Ordnung, DSC initialisiert ) moegliche Zustaende ( 1 --&gt; passiv ) moegliche Zustaende ( 2 --&gt; defekt ) moegliche Zustaende ( 4 --&gt; Traktionsmodus ) moegliche Zustaende ( 6 --&gt; Unterspannung DSC ) moegliche Zustaende ( 7 --&gt; Signal ungueltig ) Gueltigkeit des DSC Signals ( 1 Byte ) |
| STAT_GUELTIGKEIT_DSC_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; GueDSC  ( 1 Byte ) |
| STAT_REGELUNG_DSC_WERT | int | moegliche Zustaende ( 0 --&gt; keine DSC Regelung ) moegliche Zustaende ( 1 --&gt; ABS Regelung ) moegliche Zustaende ( 2 --&gt; ASC Regelung ) moegliche Zustaende ( 4 --&gt; DSC Regelung ) moegliche Zustaende ( 8 --&gt; HBA Regelung ) moegliche Zustaende ( 16 --&gt; MSR Regelung ) moegliche Zustaende ( 32 --&gt; EBV Regelung ) Gueltigkeit des DSC Signals ( 1 Byte ) |
| STAT_REGELUNG_DSC_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; RegelDSC  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-winkelwerte"></a>
### STATUS_WINKELWERTE

Auslesen verschiedener Winkelwerte, wie Fahrerlenkwinkel,Summenlenkwinkel,Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier $0F InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber PT-CAN Laenge: ( 2 Byte ) Wertebereich[+-500] |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit [Grad] |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom MPC ( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC_EINH | string | Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom NEC( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC_EINH | string | Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT | real | Motorlagewinkel Absoultwert in Grad eingelesen von ASCET( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT_EINH | string | Grad |
| STAT_SUMMENLENKWINKEL_WERT | real | LO-CAN (FahrwerkCAN) Wert des Summenlenkwinkels ( 2 Byte ) Auslesen des Summenlenkwinkels, Rohwert oder physikalischer Wert vom Summenlenkwinkelsensor LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN Wertebereich -90...+90 Einheit[Grad] |
| STAT_SUMMENLENKWINKEL_EINH | string | Einheit [Winkelgrad] Grad |
| STAT_SUMMENLENKWINKEL_ABSOLUT_WERT | real | PT-CAN (PowerTrain CAN) Wert des absoluten Summenlenkwinkels ( 2 Byte ) vorzeichnenbehafteter Wert, Skalierung (180/4096, Wertebereich bis ca +-1500 Grad) von ASCET berechnet Einheit[Grad] |
| STAT_SUMMENLENKWINKEL_ABSOLUT_EINH | string | Einheit [Winkelgrad] Grad |
| STAT_LENKRADWINKELSCHIEFSTAND_WERT | real | Lenkradwinkelschiefstand von ASCET Var. MSG_R_DiffLwGLwvirt ( 4 Byte ) Rohwert in rad |
| STAT_LENKRADWINKELSCHIEFSTAND_EINH | string | Grad Fahrerwinkel |
| STAT_ABWEICHUNG_MOTORWINKEL_WERT | real | Abweichung Motorwinkel von ASCET Var. MSG_R_LwDMdiffabs_filt ( 4 Byte ) Skalierung 1 |
| STAT_ABWEICHUNG_MOTORWINKEL_EINH | string | Grad Fahrerwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-phasenspannungen"></a>
### STATUS_PHASENSPANNUNGEN

Auslesen der Phasenspannungen U1 - U3 KWP2000: $30 InputOutputControlByLocalIdentifier $10 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHASENSPANNUNG_U1_WERT | real | Spannungen am Steller ( 2 Byte ) Einheit[V] |
| STAT_PHASENSPANNUNG_U2_WERT | real | Spannungen am Steller ( 2 Byte ) Einheit[V] |
| STAT_PHASENSPANNUNG_U3_WERT | real | Spannungen am Steller ( 2 Byte ) Einheit[V] |
| STAT_PHASENSPANNUNG_EINH | string | Einheit [Spannungen] Volt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-qualifier"></a>
### STATUS_QUALIFIER

Auslesen verschiedener ASCET Qualifier KWP2000: $30 InputOutputControlByLocalIdentifier $11 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QUERBESCH_QUAL_WERT | int | ASCET Querbeschleunigungs Qualifier 'MSG_I_Ay_qual' Laenge 1 Byte |
| STAT_QUERBESCH_QUAL_HEX | string | ASCET Querbeschleunigungs Qualifier 'MSG_I_Ay_qual' (1 Byte) |
| STAT_GIERGESCHW_QUAL_WERT | int | ASCET Giergeschwindigkeits Qualifier 'MSG_I_RR_qual' Laenge 1 Byte |
| STAT_GIERGESCHW_QUAL_HEX | string | ASCET Giergeschwindigkeits Qualifier 'MSG_I_RR_qual' (1 Byte) |
| STAT_REFGESCHW_AFS_QUAL_WERT | int | ASCET Referenzgeschwindigkeits AFS Qualifier 'MSG_I_Vx_qual' Laenge 1 Byte |
| STAT_REFGESCHW_AFS_QUAL_HEX | string | ASCET Referenzgeschwindigkeits AFS Qualifier 'MSG_I_Vx_qual' (1 Byte) |
| STAT_SUMMENLENKWINKEL_QUAL_WERT | int | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' Laenge 1 Byte |
| STAT_SUMMENLENKWINKEL_QUAL_HEX | string | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' (1 Byte) |
| STAT_FAHRERLENKWINKEL_QUAL_WERT | int | ASCET Fahrerlenkwinkel Qualifier 'MSG_I_LwDS_qual' Laenge 1 Byte |
| STAT_FAHRERLENKWINKEL_QUAL_HEX | string | ASCET Fahrerlenkwinkel Qualifier 'MSG_I_LwDS_qual' (1 Byte) |
| STAT_MOTORDYNAMIK_QUAL_WERT | int | ASCET Motordynamik Qualifier 'MSG_I_Motordynamik_qual' Laenge 1 Byte |
| STAT_MOTORDYNAMIK_QUAL_HEX | string | ASCET Motordynamik Qualifier 'MSG_I_Motordynamik_qual' (1 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-klemmen-info"></a>
### STATUS_KLEMMEN_INFO

Auslesen verschiedener Klemmenstati KWP2000: $30 InputOutputControlByLocalIdentifier $12 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME_15_CAN_WERT | int | Status Klemme 15 ( 1 Byte ) |
| STAT_KLEMME_15_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus |
| STAT_KLEMME_15_CAN_ERROR_WERT | int | Status Klemme 15 ( 1 Byte ) moegliche Faelle 0 --&gt; i.o 2 --&gt; init 4 --&gt; timeout 8 --&gt; plausibel |
| STAT_KLEMME_15_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| STAT_KLEMME_R_CAN_WERT | int | Status Klemme R ( 1 Byte ) |
| STAT_KLEMME_R_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus |
| STAT_KLEMME_R_CAN_ERROR_WERT | int | Status Klemme R ( 1 Byte ) moegliche Faelle 0 --&gt; i.o 2 --&gt; init 4 --&gt; timeout 8 --&gt; plausibel |
| STAT_KLEMME_R_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| STAT_KLEMME_50_CAN_WERT | int | Status Klemme 50 ( 1 Byte ) |
| STAT_KLEMME_50_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus |
| STAT_KLEMME_50_CAN_ERROR_WERT | int | Status Klemme 50 ( 1 Byte ) moegliche Faelle 0 --&gt; i.o 2 --&gt; init 4 --&gt; timeout 8 --&gt; plausibel |
| STAT_KLEMME_50_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-alive-info"></a>
### STATUS_ALIVE_INFO

Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier $13InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AFS_ALIVE | int | Zaehlerwert zwischen 0 ... 14 vom SG |
| STAT_FAHRER_LENKWINKEL_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des Fahrerlenkwinkels vom SZL ueber NEC eingelesen (0..14) |
| STAT_DSC_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte, nur die oberen 4 Bit gueltig ) Alivezaehler des DSC (0..14) |
| STAT_FAHRER_LENKWINKEL_ALIVECOUNTER_FWCAN_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des Fahrerlenkwinkels vom SZL ueber FW-CAN, als ASCET Var. (0..14) |
| STAT_FAHRER_LENKWINKEL_ALIVECOUNTER_SERIELL_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des Fahrerlenkwinkels vom SZL ueber serielle Ltg., als ASCET Var. (0..14) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-afs"></a>
### STATUS_AFS

Auslesen verschiedener SG Stati KWP2000: $30 InputOutputControlByLocalIdentifier $14 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME15_WERT | int | Zustand Klemme 15 Ein/Aus ( 1 Byte ) |
| STAT_KLEMME15_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus |
| STAT_SELBSTHALT_WERT | int | Zustand Selbshalt Ein/Aus |
| STAT_SELBSTHALT_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| STAT_RESET_CAN_WERT | int | Zustand CAN Bus Ein/Aus |
| STAT_RESET_CAN_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| STAT_ENDSTUFE_WERT | int | Zustand Endsufe Ein/Aus, inverse Logik |
| STAT_ENDSTUFE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; AusEin  ( 1 Byte ) |
| STAT_RELAIS_WERT | int | Zustand Relais Ein/Aus, inverse Logik |
| STAT_RELAIS_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; AusEin  ( 1 Byte ) |
| STAT_BREMSE_WERT | int | Zustand Bremse Ein/Aus |
| STAT_BREMSE_TEXT | string | Textausgabe ueber Tabellenzugriff, 'Sperre'( 1 Byte ) moegliche Zustaende 0 --&gt; Brake, (Sperre geschlossen) moegliche Zustaende 1 --&gt; PulsStart, (Stromimpuls starten, Sperre oeffnen starten) moegliche Zustaende 2 --&gt; Puls, (Stromimpuls aktiv, Sperre oeffnet) moegliche Zustaende 3 --&gt; Release, (Haltestrom, Sperre geoeffnet, Normalzustand) moegliche Zustaende 4 --&gt; BrakeStart, (Wartezeit bis Motor auslaeuft starten) moegliche Zustaende 5 --&gt; BrakeWait, (Warten bis Motor steht, fixe Zeit) |
| STAT_GUELTIGKEIT_ROTORPOSITION_WERT | int | moegliche Zustaende ( 0 --&gt; NICHT gueltig ) moegliche Zustaende ( 1 --&gt; gueltig ) moegliche Zustaende ( 2 --&gt; nicht definiert ) |
| STAT_GUELTIGKEIT_ROTORPOSITION_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; NICHT gueltig ) moegliche Zustaende ( 1 --&gt; gueltig ) Gueltigkeit des Summenlenkwinkelsensorsignals gueltig/ungueltig ( 1 Byte ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; GueLwS  ( 1 Byte ) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; in Ordnung, SZL initialisiert ) moegliche Zustaende ( 1 --&gt; SZL muss noch aufgesetzt werden, Initialisierung noch durchzufuehren ) moegliche Zustaende ( 2 --&gt; nicht definiert ) Gueltigkeit des Fahrerlenkwinkels vom SZL gueltig/ungueltig, ( 1 Byte ) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; GueLwD  ( 1 Byte ) |
| STAT_MOTORDYNAMIK_WERT | int | moegliche Zustaende ( 0 --&gt; in Ordnung, volle Dynamik ) moegliche Zustaende ( 1 --&gt; erste Schwelle ueberschritten ) moegliche Zustaende ( 3 --&gt; keine Dynamik ) ASCET Variable 'MSG_I_Motordynamic_qual' ( 1 Byte ) |
| STAT_MOTORDYNAMIK_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; MotorDyn  ( 1 Byte ) |
| STAT_VERBRENNUNGSMOTOR_WERT | int | moegliche Zustaende ( 0 --&gt; aus ) moegliche Zustaende ( 1 --&gt; ein ) ASCET Variable 'MSG_B_EngineRun_PT' ( 1 Byte ) |
| STAT_VERBRENNUNGSMOTOR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| STAT_FN_AFS_WERT | int | moegliche Zustaende ( 0...15 ) Bit0 --&gt; 0 AFS vollaktiv Bit0 --&gt; 1 AFS passiv Bit1 --&gt; 0 Gierratenregeleung aktiv Bit1 --&gt; 1 Gierratenregeleung passiv Bit2 --&gt; 0 variable Lenkuebersetzung NICHT eingeschraenkt Bit2 --&gt; 1 variable Lenkuebersetzung eingeschraenkt Bit3 --&gt; 0 variable Lenkuebersetzung aktiv Bit3 --&gt; 1 variable Lenkuebersetzung passiv ASCET Variable 'I_STATUS_FN_AFS' ( 1 Byte ) |
| STAT_FN_AFS_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; BitFktAFS  ( 1 Byte ) |
| STAT_FN_AFS_TEXT_BIT_0 | string | Textausgabe ueber Tabellenzugriff, --&gt; BitFktAFS  ( 1 Byte ) |
| STAT_FN_AFS_TEXT_BIT_1 | string | Textausgabe ueber Tabellenzugriff, --&gt; BitFktAFS  ( 1 Byte ) |
| STAT_FN_AFS_TEXT_BIT_2 | string | Textausgabe ueber Tabellenzugriff, --&gt; BitFktAFS  ( 1 Byte ) |
| STAT_FN_AFS_TEXT_BIT_3 | string | Textausgabe ueber Tabellenzugriff, --&gt; BitFktAFS  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-fehler-signale"></a>
### STATUS_CAN_FEHLER_SIGNALE

Auslesen verschiedener CAN Signalfehlerzustaende KWP2000: $30 InputOutputControlByLocalIdentifier $15 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CAN_FEHLER_SUMMENLENKWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; i.o ) moegliche Zustaende ( 2 --&gt; init ) moegliche Zustaende ( 4 --&gt; timeout ) moegliche Zustaende ( 8 --&gt; plausibel ) CAN Fehlerzustaende des Summenlenkwinkels ( 1 Byte ) |
| STAT_CAN_FEHLER_SUMMENLENKWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKELGESCHW_WERT | int | moegliche Zustaende ( 0 --&gt; i.o ) moegliche Zustaende ( 2 --&gt; init ) moegliche Zustaende ( 4 --&gt; timeout ) moegliche Zustaende ( 8 --&gt; plausibel ) CAN Fehlerzustaende des Summenlenkwinkels ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKELGESCHW_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; i.o ) moegliche Zustaende ( 2 --&gt; init ) moegliche Zustaende ( 4 --&gt; timeout ) moegliche Zustaende ( 8 --&gt; plausibel ) CAN Fehlerzustaende des Summenlenkwinkels ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_KILOMETERSTAND_WERT | int | moegliche Zustaende ( 0 --&gt; i.o ) moegliche Zustaende ( 2 --&gt; init ) moegliche Zustaende ( 4 --&gt; timeout ) moegliche Zustaende ( 8 --&gt; plausibel ) CAN Fehlerzustaende des Summenlenkwinkels ( 1 Byte ) |
| STAT_CAN_FEHLER_KILOMETERSTAND_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_FGNR_WERT | int | moegliche Zustaende ( 0 --&gt; i.o ) moegliche Zustaende ( 2 --&gt; init ) moegliche Zustaende ( 4 --&gt; timeout ) moegliche Zustaende ( 8 --&gt; plausibel ) CAN Fehlerzustaende des Summenlenkwinkels ( 1 Byte ) |
| STAT_CAN_FEHLER_FGNR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-ptcan-signale"></a>
### STATUS_PTCAN_SIGNALE

Auslesen verschiedener PT-CAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier $16 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PTCAN_FAHRGESTELLNR | string | vom AFS eingelesene Fahrgestellnummer ueber PT-CAN Botschaft ID ( 380 hex ), wird vom CAS versendet |
| STAT_PTCAN_FAHRGESTELLNR_HEX | string | Hexdarstellung des PT-CAN Signals Fahrgestellummer ( 8 Byte ) Botschaft ID ( 380 hex ), wird vom CAS versendet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-dynamik"></a>
### STATUS_DYNAMIK

Auslesen verschiedener PT-CAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier $17 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEM_MPC555_AKTUELL | int | aktueller Systemstatus des MPC gueltige Werte 0 bis 6 POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 |
| STAT_SYSTEM_MPC555_AKTUELL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_NEC_AKTUELL | int | aktueller Systemstatus des NEC gueltige Werte 0 bis 6 POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 |
| STAT_SYSTEM_NEC_AKTUELL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_MPC555_DESIRE | int | gewuenschter Status des MPC gueltige Werte 0 bis ? |
| STAT_SYSTEM_MPC555_DESIRE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_NEC_DESIRE | int | gewuenschter Status des NEC gueltige Werte 0 bis ? |
| STAT_SYSTEM_NEC_DESIRE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SUMMENLENKWINKEL_QUAL_WERT | int | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' Laenge 1 Byte |
| STAT_SUMMENLENKWINKEL_QUAL_HEX | string | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' (1 Byte) |
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber PT-CAN Laenge: ( 2 Byte ) Wertebereich[+-500] |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit [Grad] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber PT-CAN Laenge: ( 2 Byte ) CAN-ID  : 196 / 0x0C4 Wertebereich[-1440Grad/s...1440Grad/s] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit [Grad/s] |
| STAT_ABWEICHUNG_MOTORWINKEL_WERT | real | Abweichung Motorwinkel von ASCET Var. MSG_R_LwDMdiffabs_filt ( 4 Byte ) Wert wird nur im NORMAL_MODE angezeigt und wenn Summenlenkwinkel Qualifier VERUNDET mit (0x08) den Wert NULL hat bei allen anderen Betriebszustaenden wird ungültig gesetzt, -1440 |
| STAT_ABWEICHUNG_MOTORWINKEL_EINH | string | Grad Fahrerwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-mpc-error-info"></a>
### STATUS_MPC_ERROR_INFO

Auslesen des MPC555 Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $30 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_FEHLER | int | Anzahl der Fehler im Fehlerspeicher (2 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-nec-error-info"></a>
### STATUS_NEC_ERROR_INFO

Auslesen des NEC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $31 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_FEHLER | int | Anzahl der Fehler im NEC Fehlerspeicher |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-motorlagewinkel-offset-lesen"></a>
### STATUS_MOTORLAGEWINKEL_OFFSET_LESEN

Auslesen des Motorlagewinkeloffsets KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 Anzahl der auszulesenden Bytes: 6 Speicher Adresse: 0x019E Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORLAGEWINKEL_OFFSET_ROH_DEZ | int | Rohwerte in Dezimaldarstellung ( 2 Byte im Telegramm ) |
| STAT_MOTORLAGEWINKEL_OFFSET_ROH_HEX | string | Rohwerte in Hexdarstellung ( 2 Byte im Telegramm ) |
| STAT_MOTORLAGEWINKEL_OFFSET_WERT | real | in Grad |
| STAT_MOTORLAGEWINKEL_OFFSET_EINH | string | in Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-motorlagewinkel-offset-schreiben"></a>
### STEUERN_MOTORLAGEWINKEL_OFFSET_SCHREIBEN

Schreiben des Motorlagewinkeloffsets an eine feste Adresse im EEProm KWP2000: $3D WriteMemoryByAddress,(WMBA) MemoryTypeIdentifier,ROMX = 2 Anzahl der zu schreibenden Bytes: 6 Speicher Adresse: 0x019E Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTORLAGEWINKEL_OFFSET_WERT | real | in Grad |
| PSW | string | Freischaltung zum Schreiben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-c-lesen"></a>
### COD_C_LESEN

Codierdaten lesen ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | mit Adresseinfo(d.h 300x) |
| EEPROM_CODIER_DATEN | binary | Daten die ins EEPROM abgelegt werden, ohne Adresseinfo(d.h 300x) |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-c-schreiben"></a>
### COD_C_SCHREIBEN

Codierdaten schreiben ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten ( es fehlen 2 Byte Laengeninfo ) |
| EEPROM_CODIER_DATEN | binary | Daten die ins EEPROM abgelegt werden, ohne Adresseinfo(d.h 300x, 2 Byte) |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-n-lesen"></a>
### COD_N_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-n-schreiben"></a>
### COD_N_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-parameter-lesen"></a>
### COD_PARAMETER_LESEN

Codierdaten lesen ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet, Block 3000 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| COD_BLOCKNUMMER_00 | string | Blocknummer in HEX-Darstellung ( 2 Byte ) |
| COD_NUTZDATENLAENGE_00 | int | Nutzdatenlaenge in Byte fuer Block 3000, hier 62 Byte ( 1 Byte ) |
| COD_INDEX_00 | int | aktueller CodierIndex, wird ueberwacht, falls NICHT identisch mit Steckbriefdaten, dann FSP Eintrag ( 1 Byte ) |
| COD_BLOCKNUMMER_01 | string | Blocknummer in HEX-Darstellung ( 2 Byte ) |
| COD_NUTZDATENLAENGE_01 | int | Nutzdatenlaenge in Byte fuer Block 3000, hier 62 Byte ( 1 Byte ) |
| COD_INDEX_01 | int | aktueller CodierIndex, wird ueberwacht, falls NICHT identisch mit Steckbriefdaten, dann FSP Eintrag ( 1 Byte ) |
| COD_DATUM | string | Codierdatum vom Band (TT.MM.JJ), Block 3000 ( 3 Byte ) |
| COD_DATENSATZ_DATUM | string | Erstelldatum des Datensatzes (TT.MM.JJJJ), Block 3000 ( 4 Byte ) |
| COD_DATENSATZ_CODIERINDEX_ABC | int | laufender Aenderungsindex, Block 3000 ( 1 Byte ) |
| COD_DATENSATZ_VARIANTE | int | zugeordnete Fahrzeug bzw. Motorvarainte, Block 3000 ( 1 Byte ) |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-fs-mpc-loeschen"></a>
### FS_MPC_LOESCHEN

NUR Fehlerspeicher des MPC loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : $FF $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-fs-nec-loeschen"></a>
### FS_NEC_LOESCHEN

NUR Fehlerspeicher des NEC loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : $FF $01

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lwg-init"></a>
### START_LWG_INIT

Start der Summenlenkwinkelinitialisierung KWP2000: $31 StartRoutineByLocalIdentifier Modus  : $50

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| LWG_INIT_IO | int | ASCET/ASSET Variable ob Init LWG akzeptiert wurde |
| LWG_BIT_0 | int | ASCET/ASSET Variable ob Init LWG erfolgreich |
| ANZAHL_FKTAUFRUFE | int | Anzahl der SG internen Fkt.durchlaeufe |
| FAHRERLENKWINKEL_QUAL_ASCET | int | ASCET/ASSET Variable ob Fahrerlenkwinkel gueltig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-eeprom-init-mpc"></a>
### START_EEPROM_INIT_MPC

MPC EEPROM initialisieren KWP2000: $31 StartRoutineByLocalIdentifier Modus  : $51 RoutineLocalIdentifer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| START_WERT | int | Anzahl der zu initialisierenden EEPROM Bloecke |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_CODIERBLOECKE | int | Anzahl der init. Codierbloecke im SG |
| ANZAHL_FKTAUFRUFE | int | Anzahl der SG internen Fkt.durchlaeufe |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lwm-ruecksetzen"></a>
### START_LWM_RUECKSETZEN

1 Telegramm Motorlagewinkels auf ungueltig setzen, durch SG RESET 2 Telegramm Status des Motorlagewinkels wird ausgelesen KWP2000: $31 RequestRoutineResultsByLocalIdentifier $54 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GUELTIGKEIT_ROTORPOSITION_WERT | int | moegliche Zustaende ( 0 --&gt; NICHT gueltig ) moegliche Zustaende ( 1 --&gt; gueltig ) moegliche Zustaende ( 2 --&gt; nicht definiert ) |
| GUELTIGKEIT_ROTORPOSITION_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG_0 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_0 | binary | Hex-Antwort von SG |
| _TEL_DATEN_0 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_DATEN_1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_DATEN_2 | binary | Hex-Antwort von SG |

<a id="job-lwm-init-abfragen"></a>
### LWM_INIT_ABFRAGEN

Gueltigkeit des Rotorlagewinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $50 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GUELTIGKEIT_ROTORPOSITION_WERT | int | moegliche Zustaende ( 0 --&gt; NICHT gueltig ) moegliche Zustaende ( 1 --&gt; gueltig ) moegliche Zustaende ( 2 --&gt; nicht definiert ) |
| GUELTIGKEIT_ROTORPOSITION_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| INBETRIEBNAHME_LWG_FERTIG | int | 0, wenn Inbetriebnahme NICHT erfolgreich 1, wenn Inbetriebnahme erfolgreich 2, nicht definiert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-lwg-init-abfragen"></a>
### LWG_INIT_ABFRAGEN

Gueltigkeit des Summenlenkwinkels auslesen Quadrantenbestimmung KWP2000: $33 RequestRoutineResultsByLocalIdentifier $51 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LWG_QUALIFIER | int | 0, gueltiger Quadrant 1, ungueltiger Quadrant |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-nec-flash-programmier-status-lesen"></a>
### NEC_FLASH_PROGRAMMIER_STATUS_LESEN

Zustand des NEC beim bzw. nach dem Flashen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $52 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NEC_FLASH_WERT | int | moegliche Zustaende ( 0 --&gt; FLASH_BOOT ) moegliche Zustaende ( 1 --&gt; FLASH_DRIVE ) moegliche Zustaende ( 2 --&gt; FLASH_BBIND ) moegliche Zustaende ( 3 --&gt; FLASH_NOT ) moegliche Zustaende ( 4 --&gt; FLASH_UNDEF ) |
| STAT_NEC_FLASH_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; NecFlash  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-nec-eeprom-lesen"></a>
### NEC_EEPROM_LESEN

NEC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0000-0x01FF NEC Speichergroesse 512 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| NEC_EEPROM_DATEN | binary | Daten die ins EEPROM abgelegt werden, ohne 3 Byte Adress Adresseinfo |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-nec-eeprom-schreiben"></a>
### NEC_EEPROM_SCHREIBEN

NEC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $3D writeMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0000-0x01FF NEC Speichergroesse 512 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| NEC_EEPROM_DATEN | binary | Daten die ins EEPROM abgelegt werden, ohne 3 Byte Adress Adresseinfo |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-mpc-eeprom-lesen"></a>
### MPC_EEPROM_LESEN

MPC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0200-0x0FFF NEC Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MPC_EEPROM_DATEN | binary | Daten die ins EEPROM abgelegt werden, ohne 3 Byte Adress Adresseinfo |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-mpc-eeprom-schreiben"></a>
### MPC_EEPROM_SCHREIBEN

MPC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $3D writeMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige MPC Speicher Adressen: 0x0200-0x0FFF MPC Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MPC_EEPROM_DATEN | binary | Daten die ins EEPROM abgelegt werden, ohne 3 Byte Adress Adresseinfo |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-sar"></a>
### FS_LESEN_SAR

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-zf-factory-daten-lesen"></a>
### ZF_FACTORY_DATEN_LESEN

MPC EEPROM Daten lesen fuer INPA Darstellung KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige MPC Speicher Adressen: 0x0200-0x0FFF EEPROM Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZF_FACTORY_MPC_EEPROM_DATEN | binary | Daten die aus dem EEPROM gelesen werden, ohne 3 Byte Adress Adresseinfo |
| ZF_FACTORY_WERK | string | Bosch/ZF Werkskennzahl, , z.B. auf SG Label( 0078 ), Laenge 2 Byte |
| ZF_FACTORY_PAM | string | Bosch/ZF Knotenkennzahl, z.B. auf SG Label( 7441 ), Laenge 2 Byte |
| ZF_FACTORY_SERIENNUMMER | string | Bosch/ZF Seriennummer, z.B. auf SG Label( 0248 ), Laenge 2 Byte |
| ZF_FACTORY_DATUM | string | Bosch/ZF Werkskennzahl, z.B. auf SG Label( 240703 ), Laenge 3 Byte |
| ZF_FACTORY_UHRZEIT | string | Bosch/ZF Werkskennzahl, ( 17:08:03 ) Laenge 3 Byte |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-dvr-teststim"></a>
### STEUERN_DVR_TESTSTIM

Teststimuli fuer diversitaeres Rechnen setzen KWP2000: $3B WriteDataByLocalIdentifier setzt Testvektoren fuers diversi. Rechnen 2 Argumente 2,5678

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_DVR_TYP | int | Wertebereich[0....255] |
| STEUERN_DVR_TEST_VEKTOR | long | Wertebereich[0...2147483648] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-dpram-teststim"></a>
### STEUERN_DPRAM_TESTSTIM

Teststimuli DX Mechanismus setzen Erweitertes KWP2000 setzen, fuer DEBUG Zwecke KWP2000: $3B WriteDataByLocalIdentifier 2 Argumente 0,2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_TYP | int | Wertebereich[0....255] |
| STEUERN_DPRAM_TEST_VEKTOR | int | Wertebereich[0..255] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (11 × 2)
- [FORTTEXTE](#table-forttexte) (63 × 2)
- [HORTTEXTE](#table-horttexte) (63 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (4 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (4 × 3)
- [HARTTEXTEERWEITERT](#table-harttexteerweitert) (4 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (5 × 5)
- [HUMWELTMATRIX](#table-humweltmatrix) (5 × 5)
- [LOWLEVEL](#table-lowlevel) (1 × 2)
- [SYSTEMSTATE](#table-systemstate) (1 × 12)
- [ERRORSTATE](#table-errorstate) (1 × 17)
- [DPSI](#table-dpsi) (1 × 17)
- [DEH](#table-deh) (1 × 17)
- [LWS](#table-lws) (1 × 17)
- [MDYN](#table-mdyn) (1 × 17)
- [FUMWELTTEXTE](#table-fumwelttexte) (94 × 9)
- [HUMWELTTEXTE](#table-humwelttexte) (94 × 9)
- [IORTTEXTE](#table-iorttexte) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [PROZESSORSTATI](#table-prozessorstati) (8 × 2)
- [CURRENTOPMODESTATI](#table-currentopmodestati) (5 × 2)
- [DPRAMSTATI](#table-dpramstati) (4 × 2)
- [EINAUS](#table-einaus) (3 × 2)
- [AUSEIN](#table-ausein) (3 × 2)
- [GUEROTOR](#table-guerotor) (4 × 2)
- [SPERRE](#table-sperre) (7 × 2)
- [BITFKTAFS](#table-bitfktafs) (8 × 4)
- [STATUSCANFEHLER](#table-statuscanfehler) (5 × 2)
- [GUELWS](#table-guelws) (3 × 2)
- [GUELWD](#table-guelwd) (4 × 2)
- [MOTORDYN](#table-motordyn) (3 × 2)
- [GUEDSC](#table-guedsc) (7 × 2)
- [REGELDSC](#table-regeldsc) (8 × 2)
- [NECFLASH](#table-necflash) (6 × 2)
- [STATUSWORTPRUEFBEDINGUNG](#table-statuswortpruefbedingung) (3 × 2)
- [STATUSWORTFEHLER](#table-statuswortfehler) (3 × 2)
- [STATUSWORTSWZYKLUS](#table-statuswortswzyklus) (3 × 2)
- [STATUSWORTFILTERUNG](#table-statuswortfilterung) (3 × 2)
- [STATUSWORTERSATZFKT](#table-statuswortersatzfkt) (3 × 2)
- [STATUSWORTFEHLERS](#table-statuswortfehlers) (3 × 2)
- [STATUSWORTSCHATTEN](#table-statuswortschatten) (3 × 2)
- [MPCFEHLERCODE](#table-mpcfehlercode) (69 × 3)
- [NECFEHLERCODE](#table-necfehlercode) (33 × 3)
- [NECFEHLERTYP](#table-necfehlertyp) (84 × 3)
- [MPCREV](#table-mpcrev) (10 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)

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
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 11 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x80 | ERROR_FAILED_DELETE_MPC |
| 0x81 | ERROR_FAILED_DELETE_NEC |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 63 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x612C | Hardwarefehler Steuergeraet |
| 0x612D | Hydraulikoeltemperatur |
| 0x612E | Fahrgestellnummernvergleich |
| 0x612F | Codierdatenfehler |
| 0x6130 | Boot- oder Flashfehler MPC |
| 0x6131 | Flashvorgang oder -Fehler NEC |
| 0x6132 | redundanter Fahrerlenkwinkel oben |
| 0x6133 | Motorspannung |
| 0x6134 | Motorstrom |
| 0x6136 | Sensorversorgung Motorlage und -position |
| 0x6137 | Motorlagesensor |
| 0x6138 | Motor- Uebertemperatur |
| 0x6139 | Fzg Ref. Geschw. oder Fahrtrichtung unsicher oder nicht verfuegbar |
| 0x613A | Versorgungsspannung Kl. 30 ( &lt; 7.5 Volt ) |
| 0x613B | Fahrdynamiksensoren |
| 0x613C | Winkelsummenbeziehung fehlerhaft |
| 0x613D | elektr. Sperrenfehler |
| 0x613E | mechanischer Sperrenfehler |
| 0x613F | Plausibilitaet Lenkwinkel-Rad (Summenlenkwinkel) |
| 0x6140 | Redundanzvergleich Fahrerlenkwinkel oben |
| 0x6141 | Motordynamikueberwachung |
| 0x6142 | ECO-Ventil im SGM |
| 0x6143 | Servoventil im SGM |
| 0x6144 | Selbsthemmungsueberwachung |
| 0x6145 | keine Ueberwachung der Winkelsummenbeziehung |
| 0x6146 | Motortemperatursensor |
| 0x6147 | Sensorversorgung Lenkwinkel-Rad (Summenlenkwinkel) |
| 0x6149 | kombinierte Lage- Drehzahlueberwachung |
| 0x614A | Motorlagewinkel nicht initialisiert |
| 0x614B | ERCOSEK Fehler |
| 0xCE84 | nicht benutzt |
| 0xCE85 | nicht benutzt |
| 0xCE86 | nicht benutzt |
| 0xCE87 | F-CAN Kommunikationsfehler |
| 0xCE88 | nicht benutzt |
| 0xCE89 | nicht benutzt |
| 0xCE8A | nicht benutzt |
| 0xCE8B | PT-CAN Kommunikationsfehler |
| 0xCE8C | nicht benutzt |
| 0xCE8D | nicht benutzt |
| 0xCE8E | nicht benutzt |
| 0xCE8F | nicht benutzt |
| 0xCE90 | nicht benutzt |
| 0xCE91 | nicht benutzt |
| 0xCE92 | nicht benutzt |
| 0xCE93 | Botschaft (Lenkradwinkel oben, ID=0C8)Initialisierungsphase |
| 0xCE94 | Botschaft (Fahrdynamiksensor 2, ID=0C7) von F-CAN |
| 0xCE95 | Botschaft (Fahrdynamiksensor 1, ID=0CB) von F-CAN |
| 0xCE96 | Botschaft (Radgeschwindigkeiten, ID=0CE) von DSC F-CAN |
| 0xCE97 | Botschaft (Lenkwinkel-Rad (Summenlenkwinkel), ID=0C3) von F-CAN |
| 0xCE98 | Botschaft (Regeleingriffe DSC, ID=11E) von DSC F-CAN |
| 0xCE99 | Botschaft (Lenkradwinkel oben, ID=0C8) von SZL F-CAN |
| 0xCE9A | Botschaft (Radtoleranzabgleich, ID=374) von DSC PT-CAN |
| 0xCE9B | Botschaft (Fahrzeugzustand, ID=1A0) von DSC PT-CAN |
| 0xCE9C | Botschaft (Status DSC, ID=19E) von DSC PT-CAN |
| 0xCE9D | Botschaft (Motormoment 1, ID=0A8) von DME PT-CAN |
| 0xCE9E | Botschaft (Motormoment 3, ID=0AA) von DME PT-CAN |
| 0xCE9F | Botschaft (Motordaten, ID=1D0) von DME PT-CAN |
| 0xCEA0 | Botschaft (Status Lenkunterstuetzung, ID=0E0) von SGM PT-CAN |
| 0xCEA1 | Botschaft (Klemmenstatus, ID=130) von CAS PT-CAN |
| 0xCEA2 | Botschaft (Fahrgestellnummer, ID=380) von CAS PT-CAN |
| 0xCEA3 | Botschaft (Kilometerstand, ID=330) von KI PT-CAN |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 63 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x612C | Hardwarefehler Steuergeraet |
| 0x612D | Hydraulikoeltemperatur |
| 0x612E | Fahrgestellnummernvergleich |
| 0x612F | Codierdatenfehler |
| 0x6130 | Boot- oder Flashfehler MPC |
| 0x6131 | Flashvorgang oder -Fehler NEC |
| 0x6132 | redundanter Fahrerlenkwinkel oben |
| 0x6133 | Motorspannung |
| 0x6134 | Motorstrom |
| 0x6136 | Sensorversorgung Motorlage und -position |
| 0x6137 | Motorlagesensor |
| 0x6138 | Motor- Uebertemperatur |
| 0x6139 | Fzg Ref. Geschw. oder Fahrtrichtung unsicher oder nicht verfuegbar |
| 0x613A | Versorgungsspannung Kl. 30 ( &lt; 7.5 Volt ) |
| 0x613B | Fahrdynamiksensoren |
| 0x613C | Winkelsummenbeziehung fehlerhaft |
| 0x613D | elektr. Sperrenfehler |
| 0x613E | mechanischer Sperrenfehler |
| 0x613F | Plausibilitaet Lenkwinkel-Rad (Summenlenkwinkel) |
| 0x6140 | Redundanzvergleich Fahrerlenkwinkel oben |
| 0x6141 | Motordynamikueberwachung |
| 0x6142 | ECO-Ventil im SGM |
| 0x6143 | Servoventil im SGM |
| 0x6144 | Selbsthemmungsueberwachung |
| 0x6145 | keine Ueberwachung der Winkelsummenbeziehung |
| 0x6146 | Motortemperatursensor |
| 0x6147 | Sensorversorgung Lenkwinkel-Rad (Summenlenkwinkel) |
| 0x6149 | kombinierte Lage- Drehzahlueberwachung |
| 0x614A | Motorlagewinkel nicht initialisiert |
| 0x614B | ERCOSEK Fehler |
| 0xCE84 | nicht benutzt |
| 0xCE85 | nicht benutzt |
| 0xCE86 | nicht benutzt |
| 0xCE87 | F-CAN Kommunikationsfehler |
| 0xCE88 | nicht benutzt |
| 0xCE89 | nicht benutzt |
| 0xCE8A | nicht benutzt |
| 0xCE8B | PT-CAN Kommunikationsfehler |
| 0xCE8C | nicht benutzt |
| 0xCE8D | nicht benutzt |
| 0xCE8E | nicht benutzt |
| 0xCE8F | nicht benutzt |
| 0xCE90 | nicht benutzt |
| 0xCE91 | nicht benutzt |
| 0xCE92 | nicht benutzt |
| 0xCE93 | Botschaft (Lenkradwinkel oben, ID=0C8)Initialisierungsphase |
| 0xCE94 | Botschaft (Fahrdynamiksensor 2, ID=0C7) von F-CAN |
| 0xCE95 | Botschaft (Fahrdynamiksensor 1, ID=0CB) von F-CAN |
| 0xCE96 | Botschaft (Radgeschwindigkeiten, ID=0CE) von DSC F-CAN |
| 0xCE97 | Botschaft (Lenkwinkel-Rad (Summenlenkwinkel), ID=0C3) von F-CAN |
| 0xCE98 | Botschaft (Regeleingriffe DSC, ID=11E) von DSC F-CAN |
| 0xCE99 | Botschaft (Lenkradwinkel oben, ID=0C8) von SZL F-CAN |
| 0xCE9A | Botschaft (Radtoleranzabgleich, ID=374) von DSC PT-CAN |
| 0xCE9B | Botschaft (Fahrzeugzustand, ID=1A0) von DSC PT-CAN |
| 0xCE9C | Botschaft (Status DSC, ID=19E) von DSC PT-CAN |
| 0xCE9D | Botschaft (Motormoment 1, ID=0A8) von DME PT-CAN |
| 0xCE9E | Botschaft (Motormoment 3, ID=0AA) von DME PT-CAN |
| 0xCE9F | Botschaft (Motordaten, ID=1D0) von DME PT-CAN |
| 0xCEA0 | Botschaft (Status Lenkunterstuetzung, ID=0E0) von SGM PT-CAN |
| 0xCEA1 | Botschaft (Klemmenstatus, ID=130) von CAS PT-CAN |
| 0xCEA2 | Botschaft (Fahrgestellnummer, ID=380) von CAS PT-CAN |
| 0xCEA3 | Botschaft (Kilometerstand, ID=330) von KI PT-CAN |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 11111111 |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 11111111 |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 00000000 | 000 | Allgemeiner Fehler |
| xxxxxx01 | 11 | Text x |
| xxxxxx10 | 12 | Text y |
| xxxxxxxx | 0 | -- |

<a id="table-harttexteerweitert"></a>
### HARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 00000000 | 000 | Allgemeiner Fehler |
| xxxxxx01 | 11 | Text x |
| xxxxxx10 | 12 | Text y |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 5 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x613B | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DPSI |
| 0x613F | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DEH |
| 0x6140 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | LWS |
| 0x6141 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | MDYN |
| default | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | 0xFF |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 5 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x613B | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DPSI |
| 0x613F | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DEH |
| 0x6140 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | LWS |
| 0x6141 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | MDYN |
| default | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | 0xFF |

<a id="table-lowlevel"></a>
### LOWLEVEL

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x01 |

<a id="table-systemstate"></a>
### SYSTEMSTATE

Dimensions: 1 rows × 12 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C |

<a id="table-errorstate"></a>
### ERRORSTATE

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x0D | 0x0E | 0x0F | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 | 0x16 | 0x17 | 0x18 | 0x19 | 0x1A | 0x1B | 0x1C |

<a id="table-dpsi"></a>
### DPSI

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x1D | 0x1E | 0x1F | 0x20 | 0x21 | 0x22 | 0x23 | 0x24 | 0x25 | 0x26 | 0x27 | 0x28 | 0x29 | 0x2A | 0x2B | 0x2C |

<a id="table-deh"></a>
### DEH

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x3D | 0x3E | 0x3F | 0x40 | 0x41 | 0x42 | 0x43 | 0x44 | 0x45 | 0x46 | 0x47 | 0x48 | 0x49 | 0x4A | 0x4B | 0x4C |

<a id="table-lws"></a>
### LWS

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x4D | 0x4E | 0x4F | 0x50 | 0x51 | 0x52 | 0x53 | 0x54 | 0x55 | 0x56 | 0x57 | 0x58 | 0x59 | 0x5A | 0x5B | 0x5C |

<a id="table-mdyn"></a>
### MDYN

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x5E | 0x5F | 0x60 | 0x61 | 0x62 | 0x63 | 0x64 | 0x65 | 0x66 | 0x67 | 0x68 | 0x69 | 0x6A | 0x6B | 0x6C | 0x6D |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 94 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | ZFLS Fehlercode | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x02 | ZFLS Fehlerart | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | Fahrzeuggeschwindigkeit | km/h | -- | signed char | -- | 2 | 1 | 0 |
| 0x04 | Querbeschleunigung | m/(s*s) | -- | signed char | -- | 1 | 7 | 0 |
| 0x05 | Gierrate | rad/s | -- | signed char | -- | 1 | 70 | 0 |
| 0x06 | Summenlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x07 | Fahrerlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x08 | Versorgungsspannung | Volt | -- | unsigned char | -- | 1 | 12.75 | 0 |
| 0x09 | Motormoment | ? | -- | signed char | -- | 1 | 1 | 0 |
| 0x0A | diverse SG-Stati | digital | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x0B | Motortemperatur | Grad Celsius | -- | unsigned char | -- | 1 | 1 | -70 |
| 0x0C | Endstufentemperatur | Grad Celsius | -- | unsigned char | -- | 1 | 1 | -70 |
| 0x0D | Abschaltung der Aktivlenkung                                        bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x0E | Abschaltung der Gierratenregelung bis Klemmenwechsel                bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x0F | Ersatzwert Motordrehzahl fuer ECO-Funktionalitaet                   bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x10 | langsame Rueckstellung des Lenkradschiefstandes nach Abschaltung    bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x11 | temporaere Abschaltung der Gierratenregelung                        bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x12 | temporaere Abschaltung der Gierratenregelung                        bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x13 | Abschaltung der Aktivlenkung nach 100 sec                           bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x14 | geschwindigkeitsunabhaengige Lenkuebersetzung                       bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x15 | fahrtrichtungsunabhaengige Lenkuebersetzung                         bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x16 | Ersatzwert Gierrate fuer Servotronic-, DME-Funktionalitaet          bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x17 | Ersatzwert Querbesch. fuer Servotronic-, DME-Funktionalitaet        bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x18 | Ersatzwert Lenkwinkelgeschw. fuer Servotronic-, DME-Funktionalitaet bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x19 | Fehler des Fahrerlenkwinkels oder des Motorlagewinkels              bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x1A | konst. Ersatzwert fuer Summenlenkwinkel                             bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x1B | Fehler des Summenlenkwinkels oder des Motorlagewinkels              bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x1C | konst. Ersatzwert fuer Fahrerlenkwinkel                             bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x1D | Sensorfehler                           FDYS bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x1E | Gradient Fehlerverdacht              FDYS bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x1F | Gradient Fehler                      FDYS bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x20 | Signal Peak Fehler                     FDYS bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x21 | Offsetueberwachung Fehler              FDYS bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x22 | Empfindlichkeits Ueberwachung Fehler   FDYS bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x23 | Roh-Redundanz Fehlerverdacht           FDYS bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x24 | Roh-Redundanz Fehler                   FDYS bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x25 | unbenutzt                              FDYS bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x26 | Referenz Redundanz Fehlerverdacht    FDYS bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x27 | Referenz Redundanz Fehler            FDYS bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x28 | unbenutzt                              FDYS bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x29 | Fehler im Sensorcluster 2              FDYS bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x2A | Fehler im Sensorcluster 1              FDYS bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x2B | unbenutzt                              FDYS bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x2C | unbenutzt                              FDYS bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x3D | Lenkwinkelgradient Fehlerverdacht     LWS bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x3E | Lenkwinkelgradient Fehler             LWS bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x3F | Lenkwinkel Peak Fehler                  LWS bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x40 | unbenutzt                               LWS bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x41 | Lenkwinkeloffset Fehlerverdacht       LWS bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x42 | Lenkwinkeloffset Fehler               LWS bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x43 | Winkelsummengleichung Fehlerverdacht  LWS bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x44 | Winkelsummengleichung Fehler          LWS bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x45 | unbenutzt                               LWS bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x46 | unbenutzt                               LWS bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x47 | unbenutzt                               LWS bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x48 | unbenutzt                               LWS bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x49 | unbenutzt                               LWS bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x4A | unbenutzt                               LWS bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x4B | unbenutzt                               LWS bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x4C | unbenutzt                               LWS bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x4D | Signal Fehler Lenkradwinkel oben       LWS bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x4E | Signal Fehler redundanter Lenkr.oben   LWS bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x4F | Timeout Fehler Lenkradwinkel oben      LWS bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x50 | Timeout Fehler redundanter Lenkr.oben  LWS bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x51 | Timeout                                LWS bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x52 | Redundant Checksum Error               LWS bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x53 | Fehler Gradient Lenkradwinkel          LWS bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x54 | Redundanz Differenz Fehler             LWS bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x55 | Sum Differenz Fehler                   LWS bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x56 | Timeout Difference Fehler              LWS bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x57 | keine Lenkwinkeldaten                  LWS bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x58 | keine Lenkwinkeldaten oben             LWS bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x59 | keine redundanten Lenkwinkeldaten      LWS bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x5A | keine Lenkwinkeldaten aus FIFO         LWS bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x5B | Timeout im FIFO                        LWS bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x5C | unbenutzt                              LWS bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x5E | Fehler Integral 1                   MDYN Bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x5F | Fehler Integral 2                   MDYN Bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x60 | unbenutzt                             MDYN Bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x61 | unbenutzt                             MDYN Bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x62 | unbenutzt                             MDYN Bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x63 | unbenutzt                             MDYN Bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x64 | unbenutzt                             MDYN Bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x65 | unbenutzt                             MDYN Bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x66 | unbenutzt                             MDYN Bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x67 | unbenutzt                             MDYN Bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x68 | unbenutzt                             MDYN Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x69 | unbenutzt                             MDYN Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x6A | unbenutzt                             MDYN Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x6B | unbenutzt                             MDYN Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x6C | unbenutzt                             MDYN Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x6D | unbenutzt                             MDYN Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0xFF | ohne Bedeutung | 1 | -- | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte UW | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 94 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | ZFLS Fehlercode | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x02 | ZFLS Fehlerart | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | Fahrzeuggeschwindigkeit | km/h | -- | signed char | -- | 2 | 1 | 0 |
| 0x04 | Querbeschleunigung | m/(s*s) | -- | signed char | -- | 1 | 7 | 0 |
| 0x05 | Gierrate | rad/s | -- | signed char | -- | 1 | 70 | 0 |
| 0x06 | Summenlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x07 | Fahrerlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x08 | Versorgungsspannung | Volt | -- | unsigned char | -- | 1 | 12.75 | 0 |
| 0x09 | Motormoment | ? | -- | signed char | -- | 1 | 1 | 0 |
| 0x0A | diverse SG-Stati | digital | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x0B | Motortemperatur | Grad Celsius | -- | unsigned char | -- | 1 | 1 | -70 |
| 0x0C | Endstufentemperatur | Grad Celsius | -- | unsigned char | -- | 1 | 1 | -70 |
| 0x0D | Abschaltung der Aktivlenkung                                        bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x0E | Abschaltung der Gierratenregelung bis Klemmenwechsel                bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x0F | Ersatzwert Motordrehzahl fuer ECO-Funktionalitaet                   bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x10 | langsame Rueckstellung des Lenkradschiefstandes nach Abschaltung    bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x11 | temporaere Abschaltung der Gierratenregelung                        bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x12 | temporaere Abschaltung der Gierratenregelung                        bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x13 | Abschaltung der Aktivlenkung nach 100 sec                           bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x14 | geschwindigkeitsunabhaengige Lenkuebersetzung                       bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x15 | fahrtrichtungsunabhaengige Lenkuebersetzung                         bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x16 | Ersatzwert Gierrate fuer Servotronic-, DME-Funktionalitaet          bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x17 | Ersatzwert Querbesch. fuer Servotronic-, DME-Funktionalitaet        bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x18 | Ersatzwert Lenkwinkelgeschw. fuer Servotronic-, DME-Funktionalitaet bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x19 | Fehler des Fahrerlenkwinkels oder des Motorlagewinkels              bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x1A | konst. Ersatzwert fuer Summenlenkwinkel                             bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x1B | Fehler des Summenlenkwinkels oder des Motorlagewinkels              bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x1C | konst. Ersatzwert fuer Fahrerlenkwinkel                             bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x1D | Sensorfehler                           FDYS bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x1E | Gradient Fehlerverdacht              FDYS bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x1F | Gradient Fehler                      FDYS bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x20 | Signal Peak Fehler                     FDYS bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x21 | Offsetueberwachung Fehler            FDYS bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x22 | Empfindlichkeits Ueberwachung Fehler FDYS bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x23 | Roh-Redundanz Fehlerverdacht         FDYS bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x24 | Roh-Redundanz Fehler                 FDYS bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x25 | unbenutzt                              FDYS bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x26 | Referenz Redundanz Fehlerverdacht    FDYS bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x27 | Referenz Redundanz Fehler            FDYS bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x28 | unbenutzt                              FDYS bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x29 | Fehler im Sensorcluster 2            FDYS bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x2A | Fehler im Sensorcluster 1            FDYS bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x2B | unbenutzt                              FDYS bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x2C | unbenutzt                              FDYS bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x3D | Lenkwinkelgradient Fehlerverdacht    LWS bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x3E | Lenkwinkelgradient Fehler            LWS bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x3F | Lenkwinkel Peak Fehler               LWS bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x40 | unbenutzt                              LWS bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x41 | Lenkwinkeloffset Fehlerverdacht      LWS bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x42 | Lenkwinkeloffset Fehler              LWS bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x43 | Winkelsummengleichung Fehlerverdacht LWS bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x44 | Winkelsummengleichung Fehler         LWS bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x45 | unbenutzt                              LWS bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x46 | unbenutzt                              LWS bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x47 | unbenutzt                              LWS bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x48 | unbenutzt                              LWS bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x49 | unbenutzt                              LWS bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x4A | unbenutzt                              LWS bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x4B | unbenutzt                              LWS bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x4C | unbenutzt                              LWS bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x4D | Signal Fehler Lenkradwinkel oben       LWS bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x4E | Signal Fehler redundanter Lenkr.oben   LWS bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x4F | Timeout Fehler Lenkradwinkel oben      LWS bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x50 | Timeout Fehler redundanter Lenkr.oben      LWS bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x51 | Timeout                                      LWS bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x52 | Redundant Checksum Error                   LWS bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x53 | Fehler Gradient Lenkradwinkel            LWS bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x54 | Redundanz Differenz Fehler               LWS bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x55 | Sum Differenz Fehler                     LWS bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x56 | Timeout Difference Fehler                LWS bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x57 | keine Lenkwinkeldaten                      LWS bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x58 | keine Lenkwinkeldaten oben               LWS bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x59 | keine redundanten Lenkwinkeldaten        LWS bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x5A | keine Lenkwinkeldaten aus FIFO             LWS bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x5B | Timeout im FIFO                            LWS bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x5C | unbenutzt                                    LWS bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x5E | Fehler Integral 1                    MDYN Bit  0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x5F | Fehler Integral 2                    MDYN Bit  1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x60 | unbenutzt                              MDYN Bit  2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x61 | unbenutzt                              MDYN Bit  3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x62 | unbenutzt                              MDYN Bit  4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x63 | unbenutzt                              MDYN Bit  5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x64 | unbenutzt                              MDYN Bit  6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x65 | unbenutzt                              MDYN Bit  7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x66 | unbenutzt                              MDYN Bit  8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x67 | unbenutzt                              MDYN Bit  9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x68 | unbenutzt                              MDYN Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x69 | unbenutzt                              MDYN Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x6A | unbenutzt                              MDYN Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x6B | unbenutzt                              MDYN Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x6C | unbenutzt                              MDYN Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x6D | unbenutzt                              MDYN Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0xFF | ohne Bedeutung | 1 | -- | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte UW | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 7 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x1001 | Fehler a |
| 0x1002 | Fehler b |
| 0x1003 | Fehler c |
| 0x1004 | Fehler d |
| 0x1005 | Fehler e |
| 0x1006 | Fehler f |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | -- | unsigned char | -- |  1 | 1 | 0 |
| 0x02 | Aussentemperatur | Grad C | -- | signed char | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-prozessorstati"></a>
### PROZESSORSTATI

Dimensions: 8 rows × 2 columns

| PROZ_STATI_NR | PROZ_STATI_TEXT |
| --- | --- |
| 0x00 | POWER_OFF |
| 0x01 | PRE_INITIALISATION |
| 0x02 | INITIALISATION |
| 0x03 | PRE_DRIVE |
| 0x04 | NORMAL_MODE |
| 0x05 | POST_RUN_MODE |
| 0x06 | ERROR_MODE |
| 0xFF | unbekannter Prozessorstatus |

<a id="table-currentopmodestati"></a>
### CURRENTOPMODESTATI

Dimensions: 5 rows × 2 columns

| COPM_STATI_NR | COPM_STATI_TEXT |
| --- | --- |
| 0x01 | SetOMInitialisation |
| 0x02 | SetOMStandBy |
| 0x03 | SetOMDrive |
| 0x04 | SetOMLimpHome |
| 0xFF | unbekannter Betriebssystemstatus |

<a id="table-dpramstati"></a>
### DPRAMSTATI

Dimensions: 4 rows × 2 columns

| DPRAM_STATI_NR | DPRAM_STATI_TEXT |
| --- | --- |
| 0x00 | n.d. |
| 0x01 | i.o. |
| 0x02 | n.i.o. |
| 0xFF | unbekannter DPRAM Status |

<a id="table-einaus"></a>
### EINAUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Aus                |
| 0x01 | Ein                |
| 0xFF | unbekannter Status |

<a id="table-ausein"></a>
### AUSEIN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ein                |
| 0x01 | Aus                |
| 0xFF | unbekannter Status |

<a id="table-guerotor"></a>
### GUEROTOR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NICHT gueltig |
| 0x01 | gueltig |
| 0x02 | nicht definiert |
| 0xFF | unbekannter Status |

<a id="table-sperre"></a>
### SPERRE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sperre geschlossen |
| 0x01 | Sperre oeffnen starten |
| 0x02 | Sperre oeffnet |
| 0x03 | Sperre geoeffnet |
| 0x04 | Wartezeit Motorauslauf, starten |
| 0x05 | Warten bis Motor steht |
| 0xFF | unbekannter Sperrenstatus |

<a id="table-bitfktafs"></a>
### BITFKTAFS

Dimensions: 8 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| BIT0_EIN | 0 | 0x01 | 0x01 |
| BIT0_AUS | 0 | 0x01 | 0x00 |
| BIT1_EIN | 0 | 0x02 | 0x02 |
| BIT1_AUS | 0 | 0x02 | 0x00 |
| BIT2_EIN | 0 | 0x04 | 0x04 |
| BIT2_AUS | 0 | 0x04 | 0x00 |
| BIT3_EIN | 0 | 0x08 | 0x08 |
| BIT3_AUS | 0 | 0x08 | 0x00 |

<a id="table-statuscanfehler"></a>
### STATUSCANFEHLER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | i.o. |
| 0x02 | init |
| 0x04 | timeout |
| 0x08 | plausibel |
| 0xFF | unbekannter CAN Fehler Status |

<a id="table-guelws"></a>
### GUELWS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NICHT gueltig |
| 0x01 | gueltig |
| 0xFF | unbekannter Status |

<a id="table-guelwd"></a>
### GUELWD

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | gueltig |
| 0x01 | NICHT gueltig |
| 0x02 | Fehler |
| 0xFF | unbekannter Status |

<a id="table-motordyn"></a>
### MOTORDYN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | i.O. volle Dynamik |
| 0x03 | Abschaltung AFS |
| 0xFF | unbekannter Status |

<a id="table-guedsc"></a>
### GUEDSC

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | i.O. |
| 0x01 | passiv |
| 0x02 | defekt |
| 0x04 | Traktionsmodus |
| 0x06 | Unterspannung DSC |
| 0x07 | Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-regeldsc"></a>
### REGELDSC

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Regelung |
| 0x01 | ABS Regelung |
| 0x02 | ASC Regelung |
| 0x04 | DSC Regelung |
| 0x08 | HBA Regelung |
| 0x10 | MSR Regelung |
| 0x20 | EBV Regelung |
| 0xFF | Signal ungueltig |

<a id="table-necflash"></a>
### NECFLASH

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | FLASH_BOOT      |
| 0x01 | FLASH_DRIVE     |
| 0x02 | FLASH_BBIND     |
| 0x03 | FLASH_NOT       |
| 0x04 | FLASH_UNDEF     |
| 0xFF | FLASH ungueltig |

<a id="table-statuswortpruefbedingung"></a>
### STATUSWORTPRUEFBEDINGUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Pruefbedingung nicht erreicht |
| 0x0001 | Pruefbedingung erreicht |
| 0xFFFF | unbekannter Fehler |

<a id="table-statuswortfehler"></a>
### STATUSWORTFEHLER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Fehler nicht vorhanden |
| 0x0002 | Fehler vorhanden |
| 0xFFFF | unbekannter Fehler |

<a id="table-statuswortswzyklus"></a>
### STATUSWORTSWZYKLUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Fehler im aktu. SW-Zyklus nicht erkannt |
| 0x0004 | Fehler im aktu. SW-Zyklus erkannt |
| 0xFFFF | unbekannter Fehler |

<a id="table-statuswortfilterung"></a>
### STATUSWORTFILTERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Fehler nach Filterung nicht vorhanden |
| 0x0008 | Fehler nach Filterung vorhanden |
| 0xFFFF | unbekannter Fehler |

<a id="table-statuswortersatzfkt"></a>
### STATUSWORTERSATZFKT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Ersatzfunktion nicht aktiv |
| 0x0010 | Ersatzfunktion aktiv |
| 0xFFFF | unbekannter Fehler |

<a id="table-statuswortfehlers"></a>
### STATUSWORTFEHLERS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | statischer Fehler |
| 0x0020 | sporadischer Fehler |
| 0xFFFF | unbekannter Fehler |

<a id="table-statuswortschatten"></a>
### STATUSWORTSCHATTEN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Fehler nicht im Shadow |
| 0x0040 | Fehler im Shadow |
| 0xFFFF | unbekannter Fehler |

<a id="table-mpcfehlercode"></a>
### MPCFEHLERCODE

Dimensions: 69 rows × 3 columns

| WERT | CODE | TEXT |
| --- | --- | --- |
| 0x0001 | KFC_NEC_ERR_1 | Error from NEC |
| 0x0002 | KFC_NEC_ERR_2 | Error from NEC |
| 0x0003 | KFC_NEC_ERR_3 | Error from NEC |
| 0x0004 | KFC_NEC_ERR_4 | Error from NEC |
| 0x0005 | KFC_NEC_ERR_5 | Error from NEC |
| 0x0006 | KFC_NEC_ERR_6 | Error from NEC |
| 0x0007 | KFC_NEC_ERR_7 | Error from NEC |
| 0x0008 | KFC_NEC_ERR_8 | Error from NEC |
| 0x0009 | KFC_PROG | Program error |
| 0x000A | KFC_COM | Communication error |
| 0x000B | KFC_EEPROMNR | Eeprom No Risk |
| 0x000C | KFC_EEPROMHR | Eeprom High Risk |
| 0x000D | KFC_KLD | KLD Position/Speed |
| 0x000E | KFC_ROM | ROM-Test |
| 0x000F | KFC_RAM | RAM-Test |
| 0x0010 | KFC_CORE | Core-Test |
| 0x0011 | KFC_VOTER_TEST | div.Rechnen-Fehler |
| 0x0012 | KFC_OS | ERCOSEK Fehler |
| 0x0013 | KFC_MLW_INVALID | Motorlagewinkel ungueltig |
| 0x0014 | KFC_VX_REF | Geschwindigkeit unklar |
| 0x0015 | KFC_DPSI1 | Gierratensensor 2 |
| 0x0016 | KFC_DPSI1_SHADOW | Gierratensensor 1 oder 2 |
| 0x0017 | KFC_DPSI2 | Gierratensensor 1 |
| 0x0018 | KFC_DPSI2_SHADOW | Gierratensensor 1 und 2 |
| 0x0019 | KFC_AY1 | Querbeschleunigungssensor 2 |
| 0x001A | KFC_AY1_SHADOW | Querbeschleunigungssensor 1 oder 2 |
| 0x001B | KFC_AY2 | Querbeschleunigungssensor 1 |
| 0x001C | KFC_AY2_SHADOW | Querbeschleunigungssensor oder Gierraten  |
| 0x001D | KFC_DEH | Lenkwinkelueberwachung |
| 0x001E | KFC_DEH_SHADOW | Lenkwinkelueberwachung |
| 0x001F | KFC_BLS | Bremslichtschalterueberwachung |
| 0x0020 | KFC_LWS | Redundanzueberwachung Lenkradwinkel oben |
| 0x0021 | KFC_MPC_POSCTRL_ERR | Motordynamikueberwachung |
| 0x0022 | KFC_VINCOMP | Fahrgestellnummernvergleich |
| 0x0023 | KFC_CONFIG | Codierdatenfehler |
| 0x0024 | KFC_MPC_BOOT_FLASH | SG haengt im Bootblock oder Flashdatenfehler |
| 0x0025 | KFC_NEC_UPDATE | NEC Prozessor macht gerade einen Update oder haengt im Update |
| 0x0026 | KFC_MPC_SCI_ERR | Redundanzvergleich Fahrerlenkwinkel oben |
| 0x0027 | KFC_SGM_ECOVALVE | Fehler ECO Ventil im SGM |
| 0x0028 | KFC_SGM_SERVOVALVE | Fehler Servo Ventil im SGM |
| 0x0029 | KFC_INIT_MPOS | NEC konnte Motorinit nicht durchfuehren (kl30 Verlust bei Fahrt) oder ist das NEC Fehler? |
| 0x002A | KFC_VOLTAGE | Ueber- oder Unterspannungsfehler |
| 0x002B | KFC_LOW_VOLTAGE | Unterspannung |
| 0x002C | KFC_LWS_FS | Winkelsummenbeziehung Fehler |
| 0x002D | KFC_LWS_FS_OFF | keine Ueberwachung der Winkelsummenbeziehung |
| 0x002E | KFC_SENSOR_DRIVE | positive Identifikation des Fahrdynamiksensors |
| 0x002F | KFC_CANA | error of CANA controller F-CAN |
| 0x0030 | KFC_CANB | error of CANB controller PT-CAN |
| 0x0031 | KFC_CANA_Y1 | Error ID Gierrate Antwort 2 |
| 0x0032 | KFC_CANA_Y2 | Error ID Gierrate Antwort |
| 0x0033 | KFC_CANA_DSC_VWHL | Error ID Radgeschwindigkeit |
| 0x0034 | KFC_CANA_LWSRAD | Error ID Summenlenkwinkel |
| 0x0035 | KFC_CANA_DSC_REGULATION | Error ID Regeleingriffe DSC AFS |
| 0x0036 | KFC_CANB_SZL_LWDS | Error ID Lenkradwinkel oben |
| 0x0037 | KFC_CANB_DSC_VWHLTOL | Error ID Radtoleranzabgleich |
| 0x0038 | KFC_CANB_DSC_VEHCOND | Error ID Regeleingriffe DSC AFS |
| 0x0039 | KFC_CANB_DSC_STAT | Error ID Status DSC |
| 0x003A | KFC_CANB_DME_TORQ1 | Error ID DME Bremslichtschalter |
| 0x003B | KFC_CANB_DME_TORQ3 | Error ID DME Motormoment |
| 0x003C | KFC_CANB_DME_MOTORDAT | Error ID DME Motordaten |
| 0x003D | KFC_CANB_SGM_UNTERST | Error ID SGM Status Lenkunterstuetzung |
| 0x003E | KFC_CANB_CAS_KLEMMEN | Error ID CAS Klemmenstatus |
| 0x003F | KFC_CANB_CAS_VIN | Error ID CAS Fahrgestellnummer |
| 0x0040 | KFC_CANB_KI_KM | Error ID KI Kilometerstand |
| 0x0041 | KFC_OELTTEMP | Error ID Hydraulikoeltemperatur |
| 0x0042 | KFC_CANB_SZL_LWDS_INIT | Error ID SZL Init Phase |
| 0x0043 | KFC_TBD11 | Error code TBD11 |
| 0x0044 | KFC_TBD12 | Error code TBD12 |
| 0xFFFF | ----------------------- | unbekannte MPC Fehlernummer |

<a id="table-necfehlercode"></a>
### NECFEHLERCODE

Dimensions: 33 rows × 3 columns

| WERT | CODE | TEXT |
| --- | --- | --- |
| 0x0000 | NKFC_OK | kein Fehler eingetragen |
| 0x0001 | NKFC_CAN | CAN |
| 0x0002 | NKFC_CCU | outputstage temperature |
| 0x0003 | NKFC_EEPROMNR | EEPROM: no security risk |
| 0x0004 | NKFC_US | sensor supply voltage |
| 0x0005 | NKFC_EPROM | ROM checksum |
| 0x0006 | NKFC_IWD | intelligent watchdog |
| 0x0007 | NKFC_COMP | compare |
| 0x0008 | NKFC_RAM | RAM |
| 0x0009 | NKFC_RELAIS | relais |
| 0x000A | NKFC_SMCURR | servomotor current |
| 0x000B | NKFC_SMPOS | servomotor positionsensor |
| 0x000C | NKFC_SMVOLT | servomotor phase voltage |
| 0x000D | NKFC_PROG | program error |
| 0x000E | NKFC_EEPROMHR | EEPROM: high security risk |
| 0x000F | NKFC_MOD_MC | module MC, program error |
| 0x0010 | NKFC_BRAKE | locking-pin |
| 0x0011 | NKFC_COMM | intercommunication error with MPC |
| 0x0012 | NKFC_MTEMP | temp. of motorsensor |
| 0x0013 | NKFC_LWSSUPP | supply for LWS |
| 0x0014 | NKFC_DPOS | desired position |
| 0x0015 | NKFC_MPC | NEC detected MPC error(Core;Mode) |
| 0x0016 | NKFC_MPC_SUBS_1 | Error from MPC |
| 0x0017 | NKFC_MPC_SUBS_2 | Error from MPC |
| 0x0018 | NKFC_MPC_SUBS_3 | Error from MPC |
| 0x0019 | NKFC_MPC_SUBS_4 | Error from MPC |
| 0x001A | NKFC_MPC_SUBS_5 | Error from MPC |
| 0x001B | NKFC_MPC_SUBS_6 | Error from MPC |
| 0x001C | NKFC_MPC_SUBS_7 | Error from MPC |
| 0x001D | NKFC_MPC_SUBS_8 | Error from MPC |
| 0x001E | NKFC_MTEMP_SENS | motortemp. sensor failed |
| 0x001F | NKFC_SELFLOCK | Selbsthemmungsueberwachung |
| 0xFFFF | ------------ | unbekannte NEC Fehlernummer |

<a id="table-necfehlertyp"></a>
### NECFEHLERTYP

Dimensions: 84 rows × 3 columns

| WERT | TYPE | TEXT |
| --- | --- | --- |
| 0x0000 | KFA_GEN | general fault type(no further fault type info) |
| 0x0001 | KFA_SCP | short circuit to plus |
| 0x0002 | KFA_SCM | short circuit to ground |
| 0x0003 | KFA_OC | open circuit |
| 0x0004 | KFA_SCPOC | short circuit to plus or open circuit |
| 0x0005 | KFA_SCMOC | short circuit to ground or open circuit |
| 0x0006 | KFA_THI | too high |
| 0x0007 | KFA_TLOW | too low |
| 0x0008 | KFA_NCHA | no change |
| 0x0009 | KFA_TMCHA | too much change |
| 0x000A | KFA_WREL | wrong relationship |
| 0x000B | KFA_WCOMB | wrong combination |
| 0x000C | KFA_WCKSM | wrong checksum |
| 0x000D | KFA_MCURR | motor current |
| 0x000E | KFA_CI_1 | interpolate characteristics program error 1 |
| 0x000F | KFA_CI_2 | interpolate characteristics program error 2 |
| 0x0010 | KFA_CC | central process program error |
| 0x0011 | KFA_TC | max torque control program error |
| 0x0012 | KFA_CMP_1 | compare error 1 ms task |
| 0x0013 | KFA_CMP_10 | compare error 10 ms task |
| 0x0014 | KFA_CMP_100 | compare error 100 ms task |
| 0x0015 | KFA_WD | watchdog error |
| 0x0016 | KFA_SPI | watchdog SPI(seriell parallel interface) error |
| 0x0017 | KFA_CNT | watchdog error counter |
| 0x0018 | KFA_STTOHI | steering torque to high |
| 0x0019 | KFA_STTOLO | steering torque to low |
| 0x001A | KFA_SC | steering controller program error |
| 0x001B | KFA_OFFSET | offset |
| 0x001C | KFA_EE_UD_I | EEPROM user data I error |
| 0x001D | KFA_EE_UD_II | EEPROM user data II error |
| 0x001E | KFA_EE_FAC | EEPROM factory data error |
| 0x001F | KFA_EE_CAL | EEPROM calibration data error |
| 0x0020 | KFA_RA_MC | range error in module MC volt |
| 0x0021 | KFA_RA_PWM | range error in module MC PWM |
| 0x0022 | KFA_PROGSEQ | program sequence |
| 0x0023 | KFA_SYSMOD | check system mode and operating system |
| 0x0024 | KFA_ERRORHANDLER | error handler cannot filter error; MPC is in error mode |
| 0x0025 | KFA_CORE | core error |
| 0x0026 | KFA_DRIVER | output stage driver error |
| 0x0027 | KFA_WR_ER | write error |
| 0x0028 | KFA_RD_ER | read error |
| 0x0029 | KFA_CAN_C | controller state |
| 0x002A | KFA_CAN_M | message state |
| 0x002B | KFA_CAN_T | timeout |
| 0x002C | KFA_ERFLAG | error flag from CAN |
| 0x002D | KFA_WD_REL | watchdog shut off; error relay |
| 0x002E | KFA_WD_OUT | watchdog shut off; error output stage |
| 0x002F | KFA_WD_RESP | incorrect response time |
| 0x0030 | KFA_ADFROZEN | frozen AD converter |
| 0x0031 | KFA_DISCHARGE | tbd. |
| 0x0032 | KFA_LKMPC | MPC can't switch off; relais SC plus |
| 0x0033 | KFA_LKNEC | NEC can't switch off |
| 0x0034 | KFA_LKWD | Module MC, program error |
| 0x0035 | KFA_I3_NOT_VALID | CG 120 can't switch off |
| 0x0036 | KFA_OCTMP | open circuit temp. sensor |
| 0x0037 | KFA_SCTMP | short circuit temp. sensor |
| 0x0038 | KFA_DXSERVER | DX Dualport RAM |
| 0x0039 | KFA_STACK | mpu Stack |
| 0x003A | KFA_GEN_1 | frozen AD converter |
| 0x003B | KFA_GEN_2 | tbd. |
| 0x003C | KFA_GEN_3 | MPC can't switch off; relais SC plus |
| 0x003D | KFA_GEN_4 | NEC can't switch off |
| 0x003E | KFA_GEN_5D | Module MC, program error |
| 0x003F | KFA_GEN_6 | CG 120 can't switch off |
| 0x0040 | KFA_GEN_7 | tbd. |
| 0x0041 | KFA_GEN_8 | tbd. |
| 0x0042 | KFA_GEN_9 | tbd. |
| 0x0043 | KFA_GEN_10 | tbd. |
| 0x0044 | KFA_POS_ERR | motorposition |
| 0x0045 | KFA_SPEED_ERR | motorspeed |
| 0x0046 | KFA_TIMEOUT | Timeout |
| 0x0047 | KFA_SIGN_CH0 | Sign change |
| 0x0048 | KFA_CL | Client |
| 0x0049 | KFA_EE_AD | EEprom Adaptive Data |
| 0x004A | KFA_PLAUS | General plausi error |
| 0x004B | KFA_CAN_ERROR_PASSIVE | CAN Bus driver passive |
| 0x004C | KFA_CAN_BUS_OFF | CAN Bus driver off |
| 0x004D | KFA_CAN_TIMEOUT | CAN Timeout |
| 0x004E | KFA_CAN_SIG_ERROR | CAN value error |
| 0x004F | KFA_VOTER_0 | calculation error |
| 0x0050 | KFA_VOTER_1 | velocitiy error |
| 0x0051 | KFA_VOTER_2 | sequence error |
| 0x0052 | KFA_VOTER_3 | synchronisation error |
| 0xFFFF | ---------------- | unbekannter NEC Fehler-Typ bzw. Art |

<a id="table-mpcrev"></a>
### MPCREV

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x3010 | RevE |
| 0x3010 | RevF |
| 0x3010 | RevG |
| 0x3020 | RevK |
| 0x3030 | RevK1 |
| 0x3031 | RevK2 |
| 0x3032 | RevK3 |
| 0x3021 | RevL |
| 0x3040 | RevM |
| 0xFFFF | unbekannte MPC Maske |

<a id="table-authentisierung"></a>
### AUTHENTISIERUNG

Dimensions: 4 rows × 2 columns

| AUTH_NR | AUTH_TEXT |
| --- | --- |
| 0x01 | Simple |
| 0x02 | Symetrisch |
| 0x03 | Asymetrisch |
| 0xFF | Keine |
