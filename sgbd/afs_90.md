# afs_90.prg

- Jobs: [141](#jobs)
- Tables: [113](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Active Front Steering für E90 |
| ORIGIN | BMW EF-61 Einberger, Reinhold |
| REVISION | 4.100 |
| AUTHOR | BMW EF-61 Einberger, Reinhold, Software & Systems EF-61 Schindlbeck, Joachim |
| COMMENT | N/A |
| PACKAGE | 1.34 |
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
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [IDENT_LESEN](#job-ident-lesen) - Identdaten KWP2000: $1A ReadECUIdentification SubID    $80 vordefinierte Tabellenstruktur auslesen Modus  : Default
- [IDENT_CUIFDT_LESEN](#job-ident-cuifdt-lesen) - CUIFDT aktuelles AIF Feld auslesen KWP2000: $1A ReadECUIdentification SubID    $86 CurrentUIFDataTable Modus  : Default
- [IDENT_PECUHN_LESEN](#job-ident-pecuhn-lesen) - Physikalische Hardware Nummer lesen, PECUHN KWP2000: $1A ReadECUIdentification SubID    $87 physicalECUHardwareNumber, PECUHN Index Modus  : Default
- [IDENT_SSECUSEN_LESEN](#job-ident-ssecusen-lesen) - Seriennummer aus EEPROM lesen KWP2000: $1A ReadECUIdentification SubID    $89 systemSupplierECUSerialNumber Modus  : Default
- [IDENT_SSS_LESEN](#job-ident-sss-lesen) - Revisionsnummer des MPC564 KWP2000: $1A ReadECUIdentification SubID    $8A systemSupplierSpecific Modus  : Default
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
- [STATUS_SZL](#job-status-szl) - Auslesen verschiedener vom SZL gesendeter Werte uebertragen ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier $06 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_LWG_WINKELWERTE_PHYSIKALISCH](#job-status-lwg-winkelwerte-physikalisch) - gefilterter Rohwert des Summenlenkwinkel vom Summenlenkwinkelsensor ueber Botschaft (C3) LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN oder auch FW-CAN KWP2000: $30 InputOutputControlByLocalIdentifier $07 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
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
- [STATUS_ALIVE_INFO](#job-status-alive-info) - Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier $13 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_AFS](#job-status-afs) - Auslesen verschiedener SG Stati KWP2000: $30 InputOutputControlByLocalIdentifier $14 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_CAN_FEHLER_SIGNALE](#job-status-can-fehler-signale) - Auslesen verschiedener CAN Signalfehlerzustaende KWP2000: $30 InputOutputControlByLocalIdentifier $15 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PTCAN_SIGNALE](#job-status-ptcan-signale) - Auslesen verschiedener PT-CAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier $16 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_DYNAMIK](#job-status-dynamik) - Auslesen verschiedener PT-CAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier $17 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ECO_STROM_MA](#job-status-eco-strom-ma) - Auslesen des aktuell anliegenden Stromes an ECO Ventil KWP2000: $30 InputOutputControlByLocalIdentifier $18 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SERVO_STROM_MA](#job-status-servo-strom-ma) - Auslesen des aktuell anliegenden Stromes an SERVO Ventil KWP2000: $30 InputOutputControlByLocalIdentifier $19 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_GMK](#job-status-gmk) - verschiedene GMK Werte KWP2000: $30 InputOutputControlByLocalIdentifier $1A InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SUMMENLENKWINKEL_SENSOR](#job-status-summenlenkwinkel-sensor) - ungefilterte Rohwerte des Summenlenkwinkelsensors ueber F-CAN, nur SINGLE TURN Wert KWP2000: $30 InputOutputControlByLocalIdentifier $1B InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MPC_ERROR_INFO](#job-status-mpc-error-info) - Auslesen des MPC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $30 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_NEC_ERROR_INFO](#job-status-nec-error-info) - Auslesen des NEC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $31 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_FSP_MPC_CONTROLFELD](#job-status-fsp-mpc-controlfeld) - Auslesen des MPC Fehlerspeicher Diagnose Kontrollfeld ZFLS Konserve, ZFLS EXCEL Tabelle KWP2000: $30 InputOutputControlByLocalIdentifier $32 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_FSP_NEC_CONTROLFELD](#job-status-fsp-nec-controlfeld) - Auslesen des NEC Fehlerspeicher Diagnose Kontrollfeld ZFLS Konserve, ZFLS EXCEL Tabelle KWP2000: $30 InputOutputControlByLocalIdentifier $33 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STEUERN_ECO_STROM_MA](#job-steuern-eco-strom-ma) - Auslesen des MPC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $20 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STEUERN_SERVO_STROM_MA](#job-steuern-servo-strom-ma) - Auslesen des MPC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $21 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STEUERN_ECOSERVO](#job-steuern-ecoservo) - KWP2000: $3B WriteDataByLocalIdentifier KWP2000: $91 SubID Freischaltung Bestromung der ECO SERVO Ventile ueber Diagnose
- [STATUS_EEPROM_SERIENNUMMER_SZL](#job-status-eeprom-seriennummer-szl) - Auslesen der im AFS EEPROM abgelegten Seriennummer des SZL AFS wird/bleibt inaktiv falls SZL getauscht wird KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdentifier(IOLI) $08 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_EEPROM_OFFSET_SZL](#job-status-eeprom-offset-szl) - Auslesen des im AFS EEPROM abgelegten Fahrerlenkwinkeloffsets vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier $02 InputOutputLocalIdentifier(IOLI) $08 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_EEPROM_SENSOREN](#job-status-eeprom-sensoren) - Sensordaten aus EEPROM lesen auch mit COTOOL32 KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdentifier(IOLI) $08 InputOutputControlParameter(IOCP) Modus  : Default
- [COD_C_LESEN](#job-cod-c-lesen) - Codierdaten lesen ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_C_SCHREIBEN](#job-cod-c-schreiben) - Codierdaten schreiben ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_N_LESEN](#job-cod-n-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_N_SCHREIBEN](#job-cod-n-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_PARAMETER_LESEN](#job-cod-parameter-lesen) - Codierdaten lesen ueber COTOOL(Loehnert) Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet, Block 3000 Modus  : Default
- [FS_MPC_LOESCHEN](#job-fs-mpc-loeschen) - NUR Fehlerspeicher des MPC loeschen KWP2000: $14 ClearDiagnosticInformation $FF,$00 Modus  : Default
- [FS_NEC_LOESCHEN](#job-fs-nec-loeschen) - NUR Fehlerspeicher des NEC loeschen KWP2000: $14 ClearDiagnosticInformation $FF $01 Modus  : Default
- [START_LWG_INIT](#job-start-lwg-init) - Start der Summenlenkwinkelinitialisierung KWP2000: $31 StartRoutineByLocalIdentifier $50 RoutineLocalIdentifier Modus  : Default
- [START_SENSORCLUSTER_OFFSET_ABGLEICH](#job-start-sensorcluster-offset-abgleich) - AFS EEPROM Sensorclusteroffsetwerte mit DEFAULT Daten beschreiben KWP2000: $31 StartRoutineByLocalIdentifier $51 RoutineLocalIdentifier Modus  : SG darf NICHT im NORMAL_MODE, Fahrzeuggeschwindigkeit kleiner 5 km/h Modus  : Zugriff auf EEPROM muss moeglich sein Modus  : um die Werte ins EEPROM zu uebenehmen MUSS SG ueber POSTRUN laufen Modus  : Wechsel Klemme 15
- [START_SUMMENLENKWINKEL_OFFSET_ABGLEICH](#job-start-summenlenkwinkel-offset-abgleich) - AFS EEPROM Summenlenkwinkeloffsetwerte mit DEFAULT Daten beschreiben KWP2000: $31 StartRoutineByLocalIdentifier $52 RoutineLocalIdentifier Modus  : SG darf NICHT im NORMAL_MODE, Fahrzeuggeschwindigkeit kleiner 5 km/h Modus  : Zugriff auf EEPROM muss moeglich sein Modus  : um die Werte ins EEPROM zu uebenehmen MUSS SG ueber POSTRUN laufen Modus  : Wechsel Klemme 15
- [START_GIERRATENEMPFINDLICHKEIT_ABGLEICH](#job-start-gierratenempfindlichkeit-abgleich) - AFS EEPROM Gierratenempfindlichkeiten mit DEFAULT Daten beschreiben KWP2000: $31 StartRoutineByLocalIdentifier $53 RoutineLocalIdentifier Modus  : SG darf NICHT im NORMAL_MODE, Fahrzeuggeschwindigkeit kleiner 5 km/h Modus  : Zugriff auf EEPROM muss moeglich sein Modus  : um die Werte ins EEPROM zu uebenehmen MUSS SG ueber POSTRUN laufen Modus  : Wechsel Klemme 15
- [START_LWM_RUECKSETZEN](#job-start-lwm-ruecksetzen) - 1 Telegramm Motorlagewinkels auf ungueltig setzen, durch SG RESET Positive Antwort NUR im PRE_DRIVE und NORMAL_MODE 2 Telegramm Status des Motorlagewinkels wird ausgelesen KWP2000: $31 RequestRoutineResultsByLocalIdentifier $54 Inbetriebnahme Resultat abfragen Modus  : Default
- [LWM_INIT_ABFRAGEN](#job-lwm-init-abfragen) - Gueltigkeit des Rotorlagewinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $50 Inbetriebnahme Resultat abfragen Modus  : Default
- [STATUS_LWG_QUADRANT_ABFRAGEN](#job-status-lwg-quadrant-abfragen) - Quadrantengueltigkeit des Summenlenkwinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $51 Modus  : Default
- [NEC_FLASH_PROGRAMMIER_STATUS_LESEN](#job-nec-flash-programmier-status-lesen) - Zustand des NEC beim bzw. nach dem Flashen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $52 Resultat anfragen Modus  : Default
- [STATUS_ADAPTIVDATEN_ABGLEICH_ABFRAGEN](#job-status-adaptivdaten-abgleich-abfragen) - aktueller Zustand des EEPROM Adaptivdatenabgleichs KWP2000: $33 RequestRoutineResultsByLocalIdentifier $53 RoutineLocalIdentifier ( RELI ) Modus  : Default
- [NEC_EEPROM_LESEN](#job-nec-eeprom-lesen) - NEC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0000-0x01FF NEC Speichergroesse 512 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [NEC_EEPROM_SCHREIBEN](#job-nec-eeprom-schreiben) - NEC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $3D writeMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0000-0x01FF NEC Speichergroesse 512 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [MPC_EEPROM_LESEN](#job-mpc-eeprom-lesen) - MPC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige NEC Speicher Adressen: 0x0200-0x0FFF NEC Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [MPC_EEPROM_SCHREIBEN](#job-mpc-eeprom-schreiben) - MPC EEPROM Daten lesen ueber COTOOL(Loehnert) KWP2000: $3D writeMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige MPC Speicher Adressen: 0x0200-0x0FFF MPC Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte Modus  : Default
- [ZF_FACTORY_DATEN_LESEN](#job-zf-factory-daten-lesen) - MPC EEPROM Daten lesen fuer INPA Darstellung KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige MPC Speicher Adressen: 0x0200-0x0FFF EEPROM Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte hier werden 12 Byte aus dem Werksdatenbereich ausgelesen, ab Adresse  0x0FCA Modus  : Default
- [STATUS_AFS_OS_UNTER_NUMMER](#job-status-afs-os-unter-nummer) - Auslesen verschiedener Betriebssystem (OS,SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID    $32 InputOutputLocalIdentifier(IOLI) SubID    $01 InputOutputControlParameter(IOCP) Modus  : Default

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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |

<a id="job-ident-lesen"></a>
### IDENT_LESEN

Identdaten KWP2000: $1A ReadECUIdentification SubID    $80 vordefinierte Tabellenstruktur auslesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| AIF_ANZ_DATEN | int | AIF Feld Typ Groesse des jeweiligen Eintrages ist aus dem Adressofset ersichtlich 0x40_hex ( 64_dez ) Power PC 0x33_hex ( 51_dez ) fuer alle anderen Anwender des grossen AIF Feldes 0x12_hex ( 18_dez ) letztmoeglicher Blockeintrag 0xFE_hex ( 254_dez ) letztmöglicher Eintrag 0x01_hex ( 64_dez ) nur ein Eintrag der aber ueberschreibbar ist 0xFF_hex ( 255_dez ) freier Speicherplatz 0x00_hex ( 00_dez ) freier Speicherplatz |
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
| AIF_RESERVE | string | Reserve fuer MPC564 |
| AIF_RESERVE_HEX | string | Speicherdarstellung/Telegrammdarstellung (13 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-pecuhn-lesen"></a>
### IDENT_PECUHN_LESEN

Physikalische Hardware Nummer lesen, PECUHN KWP2000: $1A ReadECUIdentification SubID    $87 physicalECUHardwareNumber, PECUHN Index Modus  : Default

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
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-sss-lesen"></a>
### IDENT_SSS_LESEN

Revisionsnummer des MPC564 KWP2000: $1A ReadECUIdentification SubID    $8A systemSupplierSpecific Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MPC564_REVISIONS_NR | string | IMMR (Internal Memory Map Register) wird ausgelesen Prozessorrevisionsnummer MPC564 2-stellig in diesem RESULT werden nur 2 Byte ausgewertet |
| MPC564_REVISIONS_NR_HEX | string | Telegrammdarstellung MPC564 Revisionsnummer (4 Byte) |
| MPC564_REVISIONS_TEXT | string | Prozessorrevisionsnummer MPC564 2-stellig in diesem RESULT werden nur 2 Byte ausgewertet in Tabelle 'MPCRev' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| INTEGRATIONS_STUFE_ALT | string | aktuelle Interationssufe z.B. 'I330'( 4 Byte ) |
| INTEGRATIONS_STUFE | string | aktuelle Interationssufe z.B. 'E89x-04-12-415'( 14 Byte ) |
| INTEGRATIONS_STUFE_HEX | string | aktuelle Interationssufe in HEX ( 14 Byte ) |
| DCM_NAME | string | aktueller DCM File Name z.B. 'Bla bla'( max. 64 Byte ) |
| DCM_NAME_HEX | string | aktueller DCM File Name ( max. 64 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| MPC_SVN | string | aktuelle MPC Softwarenummer der ZFLS Lib auf MPC Seite( 11 Byte ) |
| NEC_SVN | string | aktuelle NEC Softwarenummer des NEC-DRIVE Programms( 11 Byte ) durch DPRAM uebermittelt |
| NEC_RES | string | aktuelle NEC Softwarenummer in den Logistikdaten Code( 3 Byte ) |
| NEC_SVN_BOOT | string | aktuelle NEC Softwarenummer des NEC-BOOT Programms( 11 Byte ) gelesen von MPC Flash Adresse 0x8BFFE0 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| ZIF_BACKUP_PROGRAMM_REFERENZ | string | PRGREFB ProgrammReferenzBackup letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_BACKUP_SG_KENNUNG | string | ZZZ |
| ZIF_BACKUP_PROJEKT | string | PPPxV |
| ZIF_BACKUP_PROGRAMM_STAND | string | BBxh |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BACKUP_BMW_HW | string | VMECUH*NB vehicleManufECUHW*NumberBackup BMW Hardware* Nummer |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| AIF_ANZ_DATEN | int | AIF Feld Typ Groesse des jeweiligen Eintrages ist aus dem Adressofset ersichtlich 0x40_hex ( 64_dez ) Power PC 0x33_hex ( 51_dez ) fuer alle anderen Anwender des grossen AIF Feldes 0x12_hex ( 18_dez ) letztmoeglicher Blockeintrag 0xFE_hex ( 254_dez ) letztmöglicher Eintrag 0x01_hex ( 64_dez ) nur ein Eintrag der aber ueberschreibbar ist 0xFF_hex ( 255_dez ) freier Speicherplatz 0x00_hex ( 00_dez ) freier Speicherplatz |
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
| AIF_RESERVE | string | Reserve fuer MPC564 |
| AIF_RESERVE_HEX | string | Speicherdarstellung/Telegrammdarstellung (13 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_KLEMME30_WERT | real | Spannung an Klemme 30 Quantisierung: (1mV) Skalierungsfaktor: (1000) Wertebereich: (0 bis 20V) Telegrammlaenge KWP: (2 Byte) |
| STAT_KLEMME30_EINH | string | Einheit: (Volt) |
| STAT_VERSORGUNG_SENSOREN_5V_WERT | real | Versorgung der 5V Sensoren Quantisierung: (1mV) Skalierungsfaktor: (1000) Wertebereich: (0 bis 5V) Telegrammlaenge KWP: (2 Byte) |
| STAT_VERSORGUNG_SENSOREN_5V_EINH | string | Einheit: (Volt) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_SYSTEM_MPC_AKTUELL | int | aktueller Systemstatus des MPC POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 Wertebereich: (0 bis 6) Telegrammlaenge KWP: (1 Byte, low Nibble) |
| STAT_SYSTEM_MPC_AKTUELL_TEXT | string | Textausgabe ueber Tabelle: 'ProzessorStati' |
| STAT_SYSTEM_NEC_AKTUELL | int | aktueller Systemstatus des NEC POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 Wertebereich: (0 bis 6) Telegrammlaenge KWP: (1 Byte, high Nibble) |
| STAT_SYSTEM_NEC_AKTUELL_TEXT | string | Textausgabe ueber Tabelle: 'ProzessorStati' |
| STAT_SYSTEM_MPC_DESIRE | int | gewuenschter Status des MPC POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 Wertebereich: (0 bis 6) Telegrammlaenge KWP: (1 Byte, low Nibble) |
| STAT_SYSTEM_MPC_DESIRE_TEXT | string | Textausgabe ueber Tabelle: 'ProzessorStati' |
| STAT_SYSTEM_NEC_DESIRE | int | gewuenschter Status des NEC POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 Wertebereich: (0 bis 6) Telegrammlaenge KWP: (1 Byte, high Nibble) |
| STAT_SYSTEM_NEC_DESIRE_TEXT | string | Textausgabe ueber Tabelle: 'ProzessorStati' |
| STAT_CURRENT_OP_MODE | int | OP Status von ERCOSEK Off = 0 Initialisation = 1 StandBy = 2 Drive = 3 LimpHome = 4 Wertebereich: (0 bis 4) Telegrammlaenge KWP: (1 Byte) |
| STAT_CURRENT_OP_MODE_TEXT | string | Textausgabe ueber Tabelle: 'CurrentOPModeStati' |
| STAT_WUNSCH_BMW_MODE_WERT | int | Status von BMW Statemachine Wertebereich: (0x01,0x02,0x04,0x08,0x10,0x20) Telegrammlaenge KWP: (1 Byte) |
| STAT_WUNSCH_BMW_MODE_TEXT | string | Textausgabe ueber Tabelle: 'BMWMode' |
| STAT_ZUENDUNG_MPC_WERT | int | Zuendung MPC Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_ZUENDUNG_MPC_TEXT | string | Textausgabe ueber Tabelle: 'EinAus' |
| STAT_ZUENDUNG_NEC_WERT | int | Zuendung MPC Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_ZUENDUNG_NEC_TEXT | string | Textausgabe ueber Tabelle: 'EinAus' |
| STAT_COMM_ERROR_WERT | int | Kommunikations zwischen MPC und NEC Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_COMM_ERROR_TEXT | string | Textausgabe ueber Tabelle: 'EinAus' |
| STAT_PREINIT_WERT | int | Status durchlaufen Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_PREINIT_TEXT | string | Textausgabe ueber Tabelle: 'Fertig' |
| STAT_INIT_1_WERT | int | Status durchlaufen Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_INIT_1_TEXT | string | Textausgabe ueber Tabelle: 'Fertig' |
| STAT_INIT_2_WERT | int | Status durchlaufen Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_INIT_2_TEXT | string | Textausgabe ueber Tabelle: 'Fertig' |
| STAT_POSTRUN_WERT | int | Status durchlaufen Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_POSTRUN_TEXT | string | Textausgabe ueber Tabelle: 'Fertig' |
| STAT_WAKE_NEC_WERT | int | Aufwach flag Wertebereich: (0,1) Telegrammlaenge KWP: (1 Byte) |
| STAT_WAKE_NEC_TEXT | string | Textausgabe ueber Tabelle: 'EinAus' |
| STAT_DXJOB_WERT | int | aktuell ausgefuehrter DX Job Wertebereich: (1 bis 22 Dez) Telegrammlaenge KWP: (1 Byte) |
| STAT_DXJOB_TEXT | string | Textausgabe ueber Tabelle: 'DXJob' |
| STAT_DXSTATUS_WERT | int | aktueller DX Status Telegrammlaenge KWP: (2 Byte) |
| STAT_DXSTATUS_WERT_HEX | string | aktueller DX Status |
| STAT_DXSTATUS_TEXT | string | Textausgabe ueber Tabelle: 'DXStatus' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_DPRAM_ZUSTAND | int | Sicherheitszustand des DPRAMs Wertebereich: (0 bis 2) Telegrammlaenge KWP: (1 Byte) |
| STAT_DPRAM_ZUSTAND_TEXT | string | Textausgabe ueber Tabelle: 'DPRAMStati' |
| STAT_DPRAM_READ_STATE | int | Sicherheitszustand des DPRAMs Wertebereich: (0 bis 2) Telegrammlaenge KWP: (1 Byte) |
| STAT_DPRAM_BIT_INTERRUPT | int | Sicherheitszustand des DPRAMs Wertebereich: (0 bis 2) Telegrammlaenge KWP: (1 Byte) |
| STAT_ROM_CHECK_SECTOR | int | wird nur hochgezaehlt wenn das SG im NORMANL Mode ist es werden 370 Sectoren der Software ueberprueft Wertebereich: (1 bis 370) Telegrammlaenge KWP: (2 Byte) |
| STAT_ROM_CHECK_SECTOR_MAX | int | Anzahl der durch den ROM Check zu pruefenden Sektoren Wertebereich: (370) Telegrammlaenge KWP: (2 Byte) |
| STAT_ROM_CHECK_AKTUELLE_SECTOR_STARTADRESSE_HEX | string | Zugriff auf ZF-LS ROM-Check Adresstabelle aktuelle gepruefter ROMcheck Sektor z.B. 57 mit Startadresse 0x0003FF18 Telegrammlaenge KWP: (4 Byte) |
| STAT_ROM_CHECK_AKTUELLE_SECTOR_ENDEADRESSE_HEX | string | Zugriff auf ZF-LS ROM-Check Adresstabelle aktuelle gepruefter ROMcheck Sektor z.B. 57 mit Endadresse 0x00040F16 Telegrammlaenge KWP: (4 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_PHASENSTROM_I1_WERT | real | Strom am Steller Quantisierung: (0.03125 pro Bit) Wertebereich: (-50 bis 50) Telegrammlaenge KWP: (2 Byte) Einheit: (Ampere) |
| STAT_PHASENSTROM_I2_WERT | real | Strom am Steller Quantisierung: (0.03125 pro Bit) Wertebereich: (-50 bis 50) Telegrammlaenge KWP: (2 Byte) Einheit: (Ampere) |
| STAT_PHASENSTROM_I3_WERT | real | Strom am Steller Quantisierung: (0.03125 pro Bit) Wertebereich: (-50 bis 50) Telegrammlaenge KWP: (2 Byte) Einheit: (Ampere) |
| STAT_PHASENSTROM_EINH | string | Einheit: (Ampere) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_MOTOR_TEMPERATUR_MPC_WERT | real | vorzeichenbehafteter Temp.Wert des Stellmotors Wertebereich: (-50 bis +185 °C) Telegrammlaenge KWP: (1 Byte) Einheit: (°C) |
| STAT_MOTOR_TEMPERATUR_NEC_WERT | real | vorzeichenbehafteter Temp.Wert des Stellmotors Wertebereich: (-50 bis +185 °C) Telegrammlaenge KWP: (1 Byte) Einheit: (°C) |
| STAT_ENDSTUFE_TEMPERATUR_NEC_WERT | real | vorzeichenbehafteter Temp.Wert der Endstufe auf der Platine gemessen Wertebereich: (-50 bis +185 °C) Telegrammlaenge KWP: (1 Byte) Einheit: (°C) |
| STAT_ENDSTUFE_TEMPERATUR_NEC_DPRAM_WERT | real | vorzeichenbehafteter Temp.Wert der Endstufe auf der Platine gemessen Wert wird ueber feste DPRAM Adresse uebergegeben Wertebereich: (-50 bis +185 °C) Telegrammlaenge KWP: (1 Byte) Einheit: (°C) |
| STAT_TEMPERATUR_EINH | string | Einheit: (Grad Celcius) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-szl"></a>
### STATUS_SZL

Auslesen verschiedener vom SZL gesendeter Werte uebertragen ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier $06 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SZL_SERIENNUMMER | string | gesendete Seriennummer des SZL ueber F-CAN Telegrammlaenge KWP: (4 Byte) |
| STAT_SZL_SERIENNUMMER_HEX | string | Telegrammwert (HEX), gesendete Seriennummer des SZL ueber F-CAN |
| STAT_SZL_FAHRERLENKWINKEL_OFFSET | string | gesendeter Offsetwert des Fahrerlenkwinkels der beim Abgleich des SZL ermittelt wurde, F-CAN Telegrammlaenge KWP: (2 Byte) |
| STAT_SZL_FAHRERLENKWINKEL_OFFSET_HEX | string | Telegrammwert,gesendeter Offsetwert des Fahrerlenkwinkels der beim Abgleich des SZL ermittelt wurde, F-CAN |
| STAT_FAHRER_LENKWINKEL_ALIVECOUNTER_WERT | int | Alivezaehler des Fahrerlenkwinkels vom SZL Wertbereich: (0..15) Telegrammlaenge KWP: (1 Byte) |
| STAT_SZL_MUX_WERT | int | SZL Mux Zaehler Wertbereich: (0..14) Telegrammlaenge KWP: (1 Byte) |
| STAT_SZL_INFO_WERT | int | SZL Prozessor Info, Ein/Zwei Prozessorsystem Telegrammlaenge KWP: (1 Byte) |
| STAT_SZL_INFO_TEXT | string | SZL Prozessor Info, Ein/Zwei Prozessorsystem Textausgabe ueber Tabelle: 'SZLProzInfo' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-lwg-winkelwerte-physikalisch"></a>
### STATUS_LWG_WINKELWERTE_PHYSIKALISCH

gefilterter Rohwert des Summenlenkwinkel vom Summenlenkwinkelsensor ueber Botschaft (C3) LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN oder auch FW-CAN KWP2000: $30 InputOutputControlByLocalIdentifier $07 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SUMMENLENKWINKEL_WERT | real | Rohwert des Summenlenkwinkels ueber F-CAN vom Summenlenkwinkelsensor Skalierungsfaktor: ((PH) = 0,25 * (HEX)  [°]) Ungueltigkeitsbezeichnung: (8000h, wenn SG im ERRORMODE) Wertebereich: (-90 Grad bis +90 Grad) CAN-ID: (195 / 0x0C3) Telegrammlaenge KWP: (2 Byte) Einheit: (Grad) |
| STAT_SUMMENLENKWINKEL_EINH | string | Einheit: (grad) |
| STAT_SUMMENLENKWINKEL_CAN_ERROR_WERT | int | Status Summenlenkwinkel moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling Telegrammlaenge KWP: (1 Byte) |
| STAT_SUMMENLENKWINKEL_CAN_ERROR_TEXT | string | Textausgabe ueber Tabelle: 'StatusCANFehler' |
| STAT_SUMMENLENKWINKEL_ALIVECOUNTER_WERT | int | Alivezaehler des Summenlenkwinkels Wertebereich: (0 bis 255) Telegrammlaenge KWP: (1 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_SUMMENLENKWINKEL_ABSOLUT_WERT | real | F-CAN (Fahrwerk CAN) Wert des multiturn Summenlenkwinkels ( 2 Byte ) vorzeichnenbehafteter Wert, Skalierung (180/4096, Wertebereich bis ca +-1500 Grad) von ASCET berechnet Einheit: (Grad) |
| STAT_SUMMENLENKWINKEL_ABSOLUT_EINH | string | Einheit: (Winkelgrad) |
| STAT_SUMMENLENKWINKEL_GESCHWINDIGKEIT_ABSOLUT_WERT | real | F-CAN (Fahrwerk CAN) Wert der absoluten Summenlenkwinkelgeschwindigkeit( 2 Byte ) vorzeichnenbehafteter Wert, Skalierung (???) von ASCET berechnet Einheit[Grad/s] |
| STAT_SUMMENLENKWINKEL_GESCHWINDIGKEIT_ABSOLUT_EINH | string | Einheit [grad/s] Grad/s |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_ABWEICHUNG_MOTORWINKEL_EINH | string | Grad Motorwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber PT-CAN Laenge Skalierungsfaktor: ((PH) = 0,04395 * (HEX)  [°/s]) Skalierungsfaktor: ((PH)[km/h] = 180/4096 * (HEX)) Ungueltigkeitsbezeichnung: (8000h) Wertebereich: (-1440Grad...1440Grad) CAN-ID: (200 / 0x0C8) Telegrammlaenge KWP: (2 Byte) Einheit: (Grad) |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit: (Grad) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; in Ordnung, SZL initialisiert ) moegliche Zustaende ( 1 --&gt; SZL muss noch aufgesetzt werden, Initialisierung noch durchzufuehren ) moegliche Zustaende ( 2 --&gt; nicht definiert ) Gueltigkeit des Fahrerlenkwinkels vom SZL gueltig/ungueltig Telegrammlaenge KWP: (1 Byte) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_TEXT | string | Telegrammlaenge KWP: (1 Byte) Textausgabe ueber Tabelle: 'GueLwD' |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkelgeschwindigkeit vom SZL gesendet ueber PT-CAN Laenge Skalierungsfaktor: ((PH) = 0,04395 * (HEX)  [°/s]) Skalierungsfaktor: ((PH)[km/h] = 180/4096 * (HEX)) Ungueltigkeitsbezeichnung: (8000h) Wertebereich: (-1440Grad/s...1440Grad/s) CAN-ID: (196 / 0x0C4) Telegrammlaenge KWP: (2 Byte) Einheit: (Grad/s) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit: (Grad/s) |
| STAT_LENKRADWINKELSCHIEFSTAND_WERT | real | Lenkradwinkelschiefstand von ASCET Var. 'MSG_R_DiffLwGLwvirt' (Telegrammrohwert in rad) Skalierungsfaktor: ((PH)[Grad/Fahrerlenkwinkel] = (180/(PI*1,32222)) * (HEX)) Telegrammlaenge KWP: (4 Byte) Einheit: (Grad Fahrerlenkwinkel) |
| STAT_LENKRADWINKELSCHIEFSTAND_EINH | string | Einheit: (Grad Fahrerlenkwinkel) Grad Fahrerwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_RAD_GESCHWINDIGKEIT_VL_WERT | real | Radgeschwindigkeit vorne links ueber F-CAN, Laenge ( 2 Byte ) CAN-ID  : 206 / 0x0CE Skalierungsfaktor (PH)[km/h] = 0,0625 * (HEX) Skalierungsfaktor (PH)[km/h] = 1/16 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-+350 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_VL_EINH | string | Einheit [km/h] |
| STAT_RAD_GESCHWINDIGKEIT_VR_WERT | real | Radgeschwindigkeit vorne rechts ueber F-CAN, Laenge ( 2 Byte ) CAN-ID  : 206 / 0x0CE Skalierungsfaktor (PH)[km/h] = 0,0625 * (HEX) Skalierungsfaktor (PH)[km/h] = 1/16 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-+350 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_VR_EINH | string | Einheit [km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HL_WERT | real | Radgeschwindigkeit hinten links ueber F-CAN, Laenge ( 2 Byte ) CAN-ID  : 206 / 0x0CE Skalierungsfaktor (PH)[km/h] = 0,0625 * (HEX) Skalierungsfaktor (PH)[km/h] = 1/16 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-+350 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HL_EINH | string | Einheit [km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HR_WERT | real | Radgeschwindigkeit hinten rechts ueber F-CAN, Laenge ( 2 Byte ) CAN-ID  : 206 / 0x0CE Skalierungsfaktor (PH)[km/h] = 0,0625 * (HEX) Skalierungsfaktor (PH)[km/h] = 1/16 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-+350 km/h] |
| STAT_RAD_GESCHWINDIGKEIT_HR_EINH | string | Einheit [km/h] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber PT-CAN Laenge ( 2 Byte ) CAN-ID  : 196 / 0x0C4 Skalierungsfaktor (PH) = 0,04395 * (HEX)  [°/s] Skalierungsfaktor (PH)[km/h] = 180/4096 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-1440Grad/s...1440Grad/s] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit [Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_1_WERT | real | Giergeschwinigkeit 1 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 205 / 0x0CD Skalierungsfaktor (PH) = 0,00286479 * (HEX)  [°/s] Skalierungsfaktor (PH)[Grad/s] = 1/350 * (HEX) Wertebereich[-75 Grad/s...75 Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_1_EINH | string | Einheit [Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_2_WERT | real | Giergeschwinigkeit 2 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 209 / 0x0D1 Skalierungsfaktor (PH) = 0,00286479 * (HEX)  [°/s] Skalierungsfaktor (PH)[Grad/s] = 1/350 * (HEX) Wertebereich[-75 Grad/s...75 Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_2_EINH | string | Einheit [Grad/s] |
| STAT_FAHRZEUG_GESCHWINDIGKEIT_WERT | real | korrigierte Fahrzeuggeschwindigkeit von ASCET 'MSG_R_Vx_corr', Laenge ( 4 Byte ) Telegrammuebertragung[m/s], Normierungsfaktor 1000 Skalierungsfaktor SGBD [km/h] = 3600/1E6 |
| STAT_FAHRZEUG_GESCHWINDIGKEIT_EINH | string | Einheit [km/h] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_QUERBESCHLEUNIGUNG_1_WERT | real | Querbeschl. 1 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 205 / 0x0CD Skalierungsfaktor (PH) = 0,009807 * (HEX) Skalierungsfaktor (PH)[m/s2] = 9.81/1000 * (HEX) Wertebereich[-16.6719 m/s2...16.6719 m/s2] |
| STAT_QUERBESCHLEUNIGUNG_1_EINH | string | Einheit [m/s*s] |
| STAT_QUERBESCHLEUNIGUNG_1_G_WERT | real | Querbeschl. 1 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 205 / 0x0CD normiert auf 9.81 Wertebereich[-1.7 g...1.7 g] |
| STAT_QUERBESCHLEUNIGUNG_1_G_EINH | string | Einheit [g] |
| STAT_QUERBESCHLEUNIGUNG_2_WERT | real | Querbeschl. 2 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 209 / 0x0D1 Skalierungsfaktor (PH) = 0,009807 * (HEX) Skalierungsfaktor (PH)[m/s2] = 9.81/1000 * (HEX) Wertebereich[-16.6719 m/s2...16.6719 m/s2] |
| STAT_QUERBESCHLEUNIGUNG_2_EINH | string | Einheit [m/s*s] |
| STAT_QUERBESCHLEUNIGUNG_2_G_WERT | real | Querbeschl. 2 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 209 / 0x0D1 normiert auf 9.81 Wertebereich[-1.7 g...1.7 g] |
| STAT_QUERBESCHLEUNIGUNG_2_G_EINH | string | Einheit [g] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_GIERGESCHWINDIGKEIT_1_WERT | real | Giergeschwinigkeit 1 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 205 / 0x0CD Skalierungsfaktor (PH) = 0,00286479 * (HEX)  [°/s] Skalierungsfaktor (PH)[Grad/s] = 1/350 * (HEX) Wertebereich[-75 Grad/s...75 Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_1_EINH | string | Einheit [Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_2_WERT | real | Giergeschwinigkeit 2 ueber F-CAN, Laenge ( 2 Byte ) CAN-ID : 209 / 0x0D1 Skalierungsfaktor (PH) = 0,00286479 * (HEX)  [°/s] Skalierungsfaktor (PH)[Grad/s] = 1/350 * (HEX) Wertebereich[-75 Grad/s...75 Grad/s] |
| STAT_GIERGESCHWINDIGKEIT_2_EINH | string | Einheit [Grad/s] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber PT-CAN Laenge ( 2 Byte ) CAN-ID  : 200 / 0x0C8 Skalierungsfaktor (PH) = 0,04395 * (HEX)  [°/s] Skalierungsfaktor (PH)[km/h] = 180/4096 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-1440Grad/s...1440Grad/s] |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit [Grad] |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom MPC ( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC_EINH | string | Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom NEC( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC_EINH | string | Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT | real | Motorlagewinkel Absoultwert in Grad eingelesen von ASCET( 4 Byte ) Skalierung 1 Grad |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT_EINH | string | Grad |
| STAT_SUMMENLENKWINKEL_WERT | real | LO-CAN (FahrwerkCAN) Wert des Summenlenkwinkels ( 2 Byte ) Auslesen des Summenlenkwinkels, Rohwert oder physikalischer Wert vom Summenlenkwinkelsensor LO-CAN, Fahrwerks-CAN, F-CAN, Private-CAN Einheit[Grad] |
| STAT_SUMMENLENKWINKEL_EINH | string | Einheit [Winkelgrad] Grad |
| STAT_SUMMENLENKWINKEL_ABSOLUT_WERT | real | PT-CAN (PowerTrain CAN) Wert des absoluten Summenlenkwinkels ( 2 Byte ) vorzeichnenbehafteter Wert, Skalierung (180/4096, Wertebereich bis ca +-1500 Grad) von ASCET berechnet Einheit[Grad] |
| STAT_SUMMENLENKWINKEL_ABSOLUT_EINH | string | Einheit [Winkelgrad] Grad |
| STAT_LENKRADWINKELSCHIEFSTAND_WERT | real | Lenkradwinkelschiefstand von ASCET Var. MSG_R_DiffLwGLwvirt ( 4 Byte ) Skalierung 1000 |
| STAT_LENKRADWINKELSCHIEFSTAND_EINH | string | Grad Fahrerlenkwinkel |
| STAT_ABWEICHUNG_MOTORWINKEL_WERT | real | Abweichung Motorwinkel von ASCET Var. MSG_R_LwDMdiffabs_filt ( 4 Byte ) Skalierung 1 |
| STAT_ABWEICHUNG_MOTORWINKEL_EINH | string | Grad Motorwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_PHASENSPANNUNG_U1_WERT | real | Spannungen am Steller ( 2 Byte ) Quantisierung '0.03125' pro Bit Einheit[V] |
| STAT_PHASENSPANNUNG_U2_WERT | real | Spannungen am Steller ( 2 Byte ) Quantisierung '0.03125' pro Bit Einheit[V] |
| STAT_PHASENSPANNUNG_U3_WERT | real | Spannungen am Steller ( 2 Byte ) Quantisierung '0.03125' pro Bit Einheit[V] |
| STAT_PHASENSPANNUNG_EINH | string | Einheit [Spannungen] Volt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_QUERBESCH_QUAL_BIT0_WERT | int | ASCET Querbeschleunigungs Qualifier Bit 0 |
| STAT_QUERBESCH_QUAL_BIT0_TEXT | string | Text zu ASCET Querbeschleunigungs Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'AYQualBit0' |
| STAT_QUERBESCH_QUAL_BIT1_WERT | int | ASCET Querbeschleunigungs Qualifier Bit 1 |
| STAT_QUERBESCH_QUAL_BIT1_TEXT | string | Text zu ASCET Querbeschleunigungs Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'AYQualBit1' |
| STAT_QUERBESCH_QUAL_BIT2_WERT | int | ASCET Querbeschleunigungs Qualifier Bit 2 |
| STAT_QUERBESCH_QUAL_BIT2_TEXT | string | Text zu ASCET Querbeschleunigungs Qualifier Bit 2 Auswertung ueber Tabellenzufriff 'AYQualBit2' |
| STAT_QUERBESCH_QUAL_BIT4_WERT | int | ASCET Querbeschleunigungs Qualifier Bit 4 |
| STAT_QUERBESCH_QUAL_BIT4_TEXT | string | Text zu ASCET Querbeschleunigungs Qualifier Bit 4 Auswertung ueber Tabellenzufriff 'AYQualBit4' |
| STAT_QUERBESCH_QUAL_BIT5_WERT | int | ASCET Querbeschleunigungs Qualifier Bit 5 |
| STAT_QUERBESCH_QUAL_BIT5_TEXT | string | Text zu ASCET Querbeschleunigungs Qualifier Bit 5 Auswertung ueber Tabellenzufriff 'AYQualBit5' |
| STAT_QUERBESCH_QUAL_HEX | string | ASCET Querbeschleunigungs Qualifier 'MSG_I_Ay_qual' (1 Byte) |
| STAT_GIERGESCHW_QUAL_WERT | int | ASCET Giergeschwindigkeits Qualifier 'MSG_I_RR_qual' Laenge 1 Byte |
| STAT_GIERGESCHW_QUAL_BIT0_WERT | int | ASCET Giergeschw. Qualifier Bit 0 |
| STAT_GIERGESCHW_QUAL_BIT0_TEXT | string | Text zu ASCET Giergeschw. Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'RRQualBit0' |
| STAT_GIERGESCHW_QUAL_BIT1_WERT | int | ASCET Giergeschw. Qualifier Bit 1 |
| STAT_GIERGESCHW_QUAL_BIT1_TEXT | string | Text zu ASCET Giergeschw. Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'RRQualBit1' |
| STAT_GIERGESCHW_QUAL_BIT2_WERT | int | ASCET Giergeschw. Qualifier Bit 2 |
| STAT_GIERGESCHW_QUAL_BIT2_TEXT | string | Text zu ASCET Giergeschw. Qualifier Bit 2 Auswertung ueber Tabellenzufriff 'RRQualBit2' |
| STAT_GIERGESCHW_QUAL_BIT3_WERT | int | ASCET Giergeschw. Qualifier Bit 3 |
| STAT_GIERGESCHW_QUAL_BIT3_TEXT | string | Text zu ASCET Giergeschw. Qualifier Bit 3 Auswertung ueber Tabellenzufriff 'RRQualBit3' |
| STAT_GIERGESCHW_QUAL_BIT4_WERT | int | ASCET Giergeschw. Qualifier Bit 4 |
| STAT_GIERGESCHW_QUAL_BIT4_TEXT | string | Text zu ASCET Giergeschw. Qualifier Bit 4 Auswertung ueber Tabellenzufriff 'RRQualBit4' |
| STAT_GIERGESCHW_QUAL_BIT5_WERT | int | ASCET Giergeschw. Qualifier Bit 5 |
| STAT_GIERGESCHW_QUAL_BIT5_TEXT | string | Text zu ASCET Giergeschw. Qualifier Bit 5 Auswertung ueber Tabellenzufriff 'RRQualBit5' |
| STAT_GIERGESCHW_QUAL_HEX | string | ASCET Giergeschwindigkeits Qualifier 'MSG_I_RR_qual' (1 Byte) |
| STAT_REFGESCHW_AFS_QUAL_WERT | int | ASCET Referenzgeschwindigkeits AFS Qualifier 'MSG_I_Vx_qual' Laenge 1 Byte |
| STAT_REFGESCHW_AFS_QUAL_BIT0_WERT | int | ASCET Referenzgeschw. Qualifier Bit 0 |
| STAT_REFGESCHW_AFS_QUAL_BIT0_TEXT | string | Text zu ASCET Referenzgeschw. Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'REFVXQualBit0' |
| STAT_REFGESCHW_AFS_QUAL_BIT1_WERT | int | ASCET Referenzgeschw. Qualifier Bit 1 |
| STAT_REFGESCHW_AFS_QUAL_BIT1_TEXT | string | Text zu ASCET Referenzgeschw. Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'REFVXQualBit1' |
| STAT_REFGESCHW_AFS_QUAL_BIT2_WERT | int | ASCET Referenzgeschw. Qualifier Bit 2 |
| STAT_REFGESCHW_AFS_QUAL_BIT2_TEXT | string | Text zu ASCET Referenzgeschw. Qualifier Bit 2 Auswertung ueber Tabellenzufriff 'REFVXQualBit2' |
| STAT_REFGESCHW_AFS_QUAL_BIT3_WERT | int | ASCET Referenzgeschw. Qualifier Bit 3 |
| STAT_REFGESCHW_AFS_QUAL_BIT3_TEXT | string | Text zu ASCET Referenzgeschw. Qualifier Bit 3 Auswertung ueber Tabellenzufriff 'REFVXQualBit3' |
| STAT_REFGESCHW_AFS_QUAL_HEX | string | ASCET Referenzgeschwindigkeits AFS Qualifier 'MSG_I_Vx_qual' (1 Byte) |
| STAT_SUMMENLENKWINKEL_QUAL_WERT | int | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' Laenge 1 Byte |
| STAT_SUMMENLENKWINKEL_QUAL_BIT0_WERT | int | ASCET Summenlenkwinkel Qualifier Bit 0 |
| STAT_SUMMENLENKWINKEL_QUAL_BIT0_TEXT | string | Text zu ASCET Summenlenkwinkel Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'LWGQualBit0' |
| STAT_SUMMENLENKWINKEL_QUAL_BIT1_WERT | int | ASCET Summenlenkwinkel Qualifier Bit 1 |
| STAT_SUMMENLENKWINKEL_QUAL_BIT1_TEXT | string | Text zu ASCET Summenlenkwinkel Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'LWGQualBit1' |
| STAT_SUMMENLENKWINKEL_QUAL_BIT2_WERT | int | ASCET Summenlenkwinkel Qualifier Bit 2 |
| STAT_SUMMENLENKWINKEL_QUAL_BIT2_TEXT | string | Text zu ASCET Summenlenkwinkel Qualifier Bit 2 Auswertung ueber Tabellenzufriff 'LWGQualBit2' |
| STAT_SUMMENLENKWINKEL_QUAL_BIT3_WERT | int | ASCET Summenlenkwinkel Qualifier Bit 3 |
| STAT_SUMMENLENKWINKEL_QUAL_BIT3_TEXT | string | Text zu ASCET Summenlenkwinkel Qualifier Bit 3 Auswertung ueber Tabellenzufriff 'LWGQualBit3' |
| STAT_SUMMENLENKWINKEL_QUAL_BIT4_WERT | int | ASCET Summenlenkwinkel Qualifier Bit 4 |
| STAT_SUMMENLENKWINKEL_QUAL_BIT4_TEXT | string | Text zu ASCET Summenlenkwinkel Qualifier Bit 4 Auswertung ueber Tabellenzufriff 'LWGQualBit4' |
| STAT_SUMMENLENKWINKEL_QUAL_BIT5_WERT | int | ASCET Summenlenkwinkel Qualifier Bit 5 |
| STAT_SUMMENLENKWINKEL_QUAL_BIT5_TEXT | string | Text zu ASCET Summenlenkwinkel Qualifier Bit 5 Auswertung ueber Tabellenzufriff 'LWGQualBit5' |
| STAT_SUMMENLENKWINKEL_QUAL_BIT6_WERT | int | ASCET Summenlenkwinkel Qualifier Bit 6 |
| STAT_SUMMENLENKWINKEL_QUAL_BIT6_TEXT | string | Text zu ASCET Summenlenkwinkel Qualifier Bit 6 Auswertung ueber Tabellenzufriff 'LWGQualBit6' |
| STAT_SUMMENLENKWINKEL_QUAL_HEX | string | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' (1 Byte) |
| STAT_FAHRERLENKWINKEL_QUAL_WERT | int | ASCET Fahrerlenkwinkel Qualifier 'MSG_I_LwDS_qual' Laenge 1 Byte |
| STAT_FAHRERLENKWINKEL_QUAL_HEX | string | ASCET Fahrerlenkwinkel Qualifier 'MSG_I_LwDS_qual' (1 Byte) |
| STAT_FAHRERLENKWINKEL_QUAL_BIT0_WERT | int | ASCET Fahrerlenkwinkel Qualifier Bit 0 |
| STAT_FAHRERLENKWINKEL_QUAL_BIT0_TEXT | string | Text zu ASCET Fahrerlenkwinkel Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'LWDSQualBit0' |
| STAT_FAHRERLENKWINKEL_QUAL_BIT1_WERT | int | ASCET Fahrerlenkwinkel Qualifier Bit 1 |
| STAT_FAHRERLENKWINKEL_QUAL_BIT1_TEXT | string | Text zu ASCET Fahrerlenkwinkel Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'LWDSQualBit1' |
| STAT_FAHRERLENKWINKEL_QUAL_BIT2_WERT | int | ASCET Fahrerlenkwinkel Qualifier Bit 2 |
| STAT_FAHRERLENKWINKEL_QUAL_BIT2_TEXT | string | Text zu ASCET Fahrerlenkwinkel Qualifier Bit 2 Auswertung ueber Tabellenzufriff 'LWDSQualBit2' |
| STAT_FAHRERLENKWINKEL_QUAL_BIT3_WERT | int | ASCET Fahrerlenkwinkel Qualifier Bit 3 |
| STAT_FAHRERLENKWINKEL_QUAL_BIT3_TEXT | string | Text zu ASCET Fahrerlenkwinkel Qualifier Bit 3 Auswertung ueber Tabellenzufriff 'LWDSQualBit3' |
| STAT_FAHRERLENKWINKEL_QUAL_BIT4_WERT | int | ASCET Fahrerlenkwinkel Qualifier Bit 4 |
| STAT_FAHRERLENKWINKEL_QUAL_BIT4_TEXT | string | Text zu ASCET Fahrerlenkwinkel Qualifier Bit 4 Auswertung ueber Tabellenzufriff 'LWDSQualBit4' |
| STAT_MOTORDYNAMIK_QUAL_WERT | int | ASCET Motordynamik Qualifier 'MSG_I_Motordynamik_qual' Laenge 1 Byte |
| STAT_MOTORDYNAMIK_QUAL_HEX | string | ASCET Motordynamik Qualifier 'MSG_I_Motordynamik_qual' (1 Byte) |
| STAT_MOTORDYNAMIK_QUAL_BIT0_WERT | int | ASCET Motordynamik Qualifier Bit 0 |
| STAT_MOTORDYNAMIK_QUAL_BIT0_TEXT | string | Text zu ASCET Motordynamik Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'MDYQualBit0' |
| STAT_MOTORDYNAMIK_QUAL_BIT1_WERT | int | ASCET Motordynamik Qualifier Bit 1 |
| STAT_MOTORDYNAMIK_QUAL_BIT1_TEXT | string | Text zu ASCET Motordynamik Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'MDYQualBit1' |
| STAT_GMK_QUAL_WERT | int | ASCET GMK Qualifier 'MSG_I_YTC_qual' Laenge 1 Byte |
| STAT_GMK_QUAL_HEX | string | ASCET GMK Qualifier 'MSG_I_YTC_qual' (1 Byte) |
| STAT_GMK_QUAL_BIT0_WERT | int | ASCET GMK Qualifier Bit 0 |
| STAT_GMK_QUAL_BIT0_TEXT | string | Text zu ASCET GMK Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'GMKQualBit0' |
| STAT_GMK_QUAL_BIT1_WERT | int | ASCET GMK Qualifier Bit 1 |
| STAT_GMK_QUAL_BIT1_TEXT | string | Text zu ASCET GMK Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'GMKQualBit1' |
| STAT_GMK_QUAL_BIT2_WERT | int | ASCET GMK Qualifier Bit 2 |
| STAT_GMK_QUAL_BIT2_TEXT | string | Text zu ASCET GMK Qualifier Bit 2 Auswertung ueber Tabellenzufriff 'GMKQualBit2' |
| STAT_GMK_QUAL_BIT3_WERT | int | ASCET GMK Qualifier Bit 3 |
| STAT_GMK_QUAL_BIT3_TEXT | string | Text zu ASCET GMK Qualifier Bit 3 Auswertung ueber Tabellenzufriff 'GMKQualBit3' |
| STAT_GMK_QUAL_BIT4_WERT | int | ASCET GMK Qualifier Bit 4 |
| STAT_GMK_QUAL_BIT4_TEXT | string | Text zu ASCET GMK Qualifier Bit 4 Auswertung ueber Tabellenzufriff 'GMKQualBit4' |
| STAT_GMK_QUAL_BIT5_WERT | int | ASCET GMK Qualifier Bit 5 |
| STAT_GMK_QUAL_BIT5_TEXT | string | Text zu ASCET GMK Qualifier Bit 5 Auswertung ueber Tabellenzufriff 'GMKQualBit5' |
| STAT_GMK_QUAL_BIT6_WERT | int | ASCET GMK Qualifier Bit 6 |
| STAT_GMK_QUAL_BIT6_TEXT | string | Text zu ASCET GMK Qualifier Bit 6 Auswertung ueber Tabellenzufriff 'GMKQualBit6' |
| STAT_GMK_QUAL_BIT7_WERT | int | ASCET GMK Qualifier Bit 7 |
| STAT_GMK_QUAL_BIT7_TEXT | string | Text zu ASCET GMK Qualifier Bit 7 Auswertung ueber Tabellenzufriff 'GMKQualBit7' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_KLEMME_15_CAN_ERROR_WERT | int | Status Klemme 15 ( 1 Byte ) moegliche Faelle moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling |
| STAT_KLEMME_15_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| STAT_KLEMME_R_CAN_WERT | int | Status Klemme R ( 1 Byte ) |
| STAT_KLEMME_R_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus |
| STAT_KLEMME_R_CAN_ERROR_WERT | int | Status Klemme R ( 1 Byte ) moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling |
| STAT_KLEMME_R_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| STAT_KLEMME_50_CAN_WERT | int | Status Klemme 50 ( 1 Byte ) |
| STAT_KLEMME_50_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus |
| STAT_KLEMME_50_CAN_ERROR_WERT | int | Status Klemme 50 ( 1 Byte ) moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling |
| STAT_KLEMME_50_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-alive-info"></a>
### STATUS_ALIVE_INFO

Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier $13 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AFS_ALIVE | int | Telegrammwert ( 1 Byte ) Zaehlerwert zwischen 0 ... 14 vom SG |
| STAT_SUMMENLENKWINKEL_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des Summenlenkwinkels (0..255) |
| STAT_DSC_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte, nur die oberen 4 Bit gueltig ) Alivezaehler des DSC (0..14) |
| STAT_FAHRER_LENKWINKEL_ALIVECOUNTER_FWCAN_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN (0..14) |
| STAT_FAHRER_LENKWINKEL_ALIVECOUNTER_SERIELL_WERT | int | Telegrammwert ( 1 Byte ) Alivezaehler des reduanten Fahrerlenkwinkels vom SZL ueber F-CAN (0..14) |
| STAT_TEILSOLLWERT_GMK_DSC_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte, nur die unteren 4 Bit gueltig ) Alivezaehler des GMK Teilsollwertes vom DSC (0..14) |
| STAT_SENSORCLUSTER_1_ALIVECOUNTER_WERT | int | Alivezaehler des Sensorclusters 1 Telegrammwert ( 1 Byte, nur die unteren 4 Bit gueltig ) CAN-ID  : 205 / 0x0CD Wertebereich[0...15] |
| STAT_SENSORCLUSTER_2_ALIVECOUNTER_WERT | int | Alivezaehler des Sensorclusters 2 Telegrammwert ( 1 Byte, nur die unteren 4 Bit gueltig ) CAN-ID  : 209 / 0x0D1 Wertebereich[0...15] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_ENDSTUFE_WERT | int | Zustand Endsufe Aus/Ein, inverse Logik |
| STAT_ENDSTUFE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; AusEin  ( 1 Byte ) |
| STAT_RELAIS_WERT | int | Zustand Relais Aus/Ein, inverse Logik |
| STAT_RELAIS_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; AusEin  ( 1 Byte ) |
| STAT_SPERRE_WERT | int | Zustand der Sperre, 0..5 |
| STAT_SPERRE_TEXT | string | Textausgabe ueber Tabellenzugriff, 'Sperre'( 1 Byte ) moegliche Zustaende 0 --&gt; Brake, (Sperre geschlossen) moegliche Zustaende 1 --&gt; PulsStart, (Stromimpuls starten, Sperre oeffnen starten) moegliche Zustaende 2 --&gt; Puls, (Stromimpuls aktiv, Sperre oeffnet) moegliche Zustaende 3 --&gt; Release, (Haltestrom, Sperre geoeffnet, Normalzustand) moegliche Zustaende 4 --&gt; BrakeStart, (Wartezeit bis Motor auslaeuft starten) moegliche Zustaende 5 --&gt; BrakeWait, (Warten bis Motor steht, fixe Zeit) |
| STAT_GUELTIGKEIT_MOTORLAGEWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; NICHT gueltig ) moegliche Zustaende ( 1 --&gt; gueltig ) moegliche Zustaende ( 2 --&gt; nicht definiert ) |
| STAT_GUELTIGKEIT_MOTORLAGEWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
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
| STAT_ERSATZMASSNAHME_HEX_WERT | string | Wert bestimmt moegliche Abschaltungen im SG ASCET Var. 'MSG_I_Ersatzmassnahme' --&gt;  ( 4 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_CAN_FEHLER_SUMMENLENKWINKEL_WERT | int | moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling CAN Fehlerzustaende des Summenlenkwinkels ( 1 Byte ) |
| STAT_CAN_FEHLER_SUMMENLENKWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKELGESCHW_WERT | int | moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling CAN Fehlerzustaende der Fahrerlenkwinkelsgeschw. ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKELGESCHW_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKEL_WERT | int | moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling CAN Fehlerzustaende des Fahrerlenkwinkels ( 1 Byte ) |
| STAT_CAN_FEHLER_FAHRERLENKWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_KILOMETERSTAND_WERT | int | moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling CAN Fehlerzustaende des Kilometerstandes ( 1 Byte ) |
| STAT_CAN_FEHLER_KILOMETERSTAND_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| STAT_CAN_FEHLER_FGNR_WERT | int | moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling CAN Fehlerzustaende der Fahrgestellnummer ( 1 Byte ) |
| STAT_CAN_FEHLER_FGNR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| STAT_SYSTEM_MPC_AKTUELL | int | aktueller Systemstatus des MPC gueltige Werte 0 bis 6 POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 |
| STAT_SYSTEM_MPC_AKTUELL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_NEC_AKTUELL | int | aktueller Systemstatus des NEC gueltige Werte 0 bis 6 POWER_OFF = 0 PRE_INITIALISATION = 1 INITIALISATION = 2 PRE_DRIVE = 3 NORMAL_MODE = 4 POST_RUN_MODE = 5 ERROR_MODE = 6 |
| STAT_SYSTEM_NEC_AKTUELL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_MPC_DESIRE | int | gewuenschter Status des MPC gueltige Werte 0 bis ? |
| STAT_SYSTEM_MPC_DESIRE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SYSTEM_NEC_DESIRE | int | gewuenschter Status des NEC gueltige Werte 0 bis ? |
| STAT_SYSTEM_NEC_DESIRE_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; ProzessorStati |
| STAT_SUMMENLENKWINKEL_QUAL_WERT | int | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' Laenge 1 Byte |
| STAT_SUMMENLENKWINKEL_QUAL_HEX | string | ASCET Summenlenkwinkel Qualifier 'MSG_I_LwG_qual' (1 Byte) |
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber PT-CAN Laenge ( 2 Byte ) CAN-ID  : 200 / 0x0C8 Skalierungsfaktor (PH) = 0,04395 * (HEX)  [°/s] Skalierungsfaktor (PH)[km/h] = 180/4096 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-1440Grad/s...1440Grad/s] |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit [Grad] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber PT-CAN Laenge ( 2 Byte ) CAN-ID  : 196 / 0x0C4 Skalierungsfaktor (PH) = 0,04395 * (HEX)  [°/s] Skalierungsfaktor (PH)[km/h] = 180/4096 * (HEX) Ungueltigkeitsbez. 8000h Wertebereich[-1440Grad/s...1440Grad/s] |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit [Grad/s] |
| STAT_ABWEICHUNG_MOTORWINKEL_WERT | real | Abweichung Motorwinkel von ASCET Var. MSG_R_LwDMdiffabs_filt ( 4 Byte ) Wert wird nur im NORMAL_MODE angezeigt und wenn Summenlenkwinkel Qualifier VERUNDET mit (0x08) den Wert NULL hat bei allen anderen Betriebszustaenden wird ungültig gesetzt, -1440 |
| STAT_ABWEICHUNG_MOTORWINKEL_EINH | string | Grad Fahrerwinkel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-eco-strom-ma"></a>
### STATUS_ECO_STROM_MA

Auslesen des aktuell anliegenden Stromes an ECO Ventil KWP2000: $30 InputOutputControlByLocalIdentifier $18 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECO_STROM_WERT | int | Strom am ECO Ventil (2 Byte) Wertebereich[0..1000 mA] |
| STAT_ECO_STROM_EINH | string | mA |
| STAT_ECO_AKTUELL | int | (1 Byte) Wert '0', Strom konnte gestellt werden Wert '87', '88', Strom konnte NICHT gestellt werden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-servo-strom-ma"></a>
### STATUS_SERVO_STROM_MA

Auslesen des aktuell anliegenden Stromes an SERVO Ventil KWP2000: $30 InputOutputControlByLocalIdentifier $19 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERVO_STROM_WERT | int | Strom am SERVO Ventil(2 Byte) Wertebereich[0..1000 mA] |
| STAT_SERVO_STROM_EINH | string | mA |
| STAT_SERVO_AKTUELL | int | (1 Byte) Wert '0', Strom konnte gestellt werden Wert '87', '88', Strom konnte NICHT gestellt werden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-gmk"></a>
### STATUS_GMK

verschiedene GMK Werte KWP2000: $30 InputOutputControlByLocalIdentifier $1A InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GMK_QUAL_WERT | int | ASCET GMK Qualifier 'MSG_I_YTC_qual' Laenge 1 Byte |
| STAT_GMK_QUAL_BIT0_WERT | int | ASCET GMK Qualifier Bit 0 |
| STAT_GMK_QUAL_BIT0_TEXT | string | Text zu ASCET GMK Qualifier Bit 0 Auswertung ueber Tabellenzufriff 'GMKQualBit0' |
| STAT_GMK_QUAL_BIT1_WERT | int | ASCET GMK Qualifier Bit 1 |
| STAT_GMK_QUAL_BIT1_TEXT | string | Text zu ASCET GMK Qualifier Bit 1 Auswertung ueber Tabellenzufriff 'GMKQualBit1' |
| STAT_GMK_QUAL_BIT2_WERT | int | ASCET GMK Qualifier Bit 2 |
| STAT_GMK_QUAL_BIT2_TEXT | string | Text zu ASCET GMK Qualifier Bit 2 Auswertung ueber Tabellenzufriff 'GMKQualBit2' |
| STAT_GMK_QUAL_BIT3_WERT | int | ASCET GMK Qualifier Bit 3 |
| STAT_GMK_QUAL_BIT3_TEXT | string | Text zu ASCET GMK Qualifier Bit 3 Auswertung ueber Tabellenzufriff 'GMKQualBit3' |
| STAT_GMK_QUAL_BIT4_WERT | int | ASCET GMK Qualifier Bit 4 |
| STAT_GMK_QUAL_BIT4_TEXT | string | Text zu ASCET GMK Qualifier Bit 4 Auswertung ueber Tabellenzufriff 'GMKQualBit4' |
| STAT_GMK_QUAL_BIT5_WERT | int | ASCET GMK Qualifier Bit 5 |
| STAT_GMK_QUAL_BIT5_TEXT | string | Text zu ASCET GMK Qualifier Bit 5 Auswertung ueber Tabellenzufriff 'GMKQualBit5' |
| STAT_GMK_QUAL_BIT6_WERT | int | ASCET GMK Qualifier Bit 6 |
| STAT_GMK_QUAL_BIT6_TEXT | string | Text zu ASCET GMK Qualifier Bit 6 Auswertung ueber Tabellenzufriff 'GMKQualBit6' |
| STAT_GMK_QUAL_BIT7_WERT | int | ASCET GMK Qualifier Bit 7 |
| STAT_GMK_QUAL_BIT7_TEXT | string | Text zu ASCET GMK Qualifier Bit 7 Auswertung ueber Tabellenzufriff 'GMKQualBit7' |
| STAT_GMK_QUAL_HEX | string | ASCET GMK Qualifier 'MSG_I_YTC_qual' (1 Byte) |
| STAT_GMK_ERRORCODE_HEX | string | ASCET GMK Errorcode 'MSG_I_YTC_ErrorCode' (2 Byte) |
| STAT_GMK_TEILSOLLWERT_DSC_ALIVECOUNTER_WERT | int | Telegrammwert ( 1 Byte, nur die unteren 4 Bit gueltig ) Alivezaehler des GMK Teilsollwertes vom DSC (0..14) |
| STAT_GMK_ENABLE_WERT | int | GMK enable/disable 'B_par_enableYMC' Laenge 1 Byte |
| STAT_GMK_AKTIV_WERT | int | GMK aktiv/passiv 'MSG_B_YTCpassiv' Laenge 1 Byte |
| STAT_GMK_AFS_WERT | int | moegliche Zustaende ( 0..3 ) --&gt; Bit '1' '0' 0   0 keine GMK-Lenkanforderung aber GMK-Fkt. 0   1 GMK-Lenkanforderung 1   0 GMK reversibel deaktiviert 1   1 GMK irreversibel deaktiviert ASCET Variable ( 1 Byte ) |
| STAT_GMK_AFS_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; BitGMKAFS  ( 1 Byte ) |
| STAT_GMK_TEILSOLLWERT_WERT | real | GMK Teilsollwert vom DSC ASCET Var. MSG_R_LwWC_YTC_FS ( 4 Byte ) Skalierung 1 |
| STAT_GMK_TEILSOLLWERT_EINH | string | Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-summenlenkwinkel-sensor"></a>
### STATUS_SUMMENLENKWINKEL_SENSOR

ungefilterte Rohwerte des Summenlenkwinkelsensors ueber F-CAN, nur SINGLE TURN Wert KWP2000: $30 InputOutputControlByLocalIdentifier $1B InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SUMMENLENKWINKEL_SENSOR_CAN_WERT | real | Rohwert des Summenlenkwinkels ueber F-CAN vom Summenlenkwinkelsensor CAN-ID  : 195 / 0x0C3 Umrechnungfaktor (PH) = 0,25 * (HEX)  [°] Wertebereich[-90 Grad...+90 Grad] Telegrammlaenge KWP, 2 Byte Einheit[Grad] |
| STAT_SUMMENLENKWINKEL_SENSOR_EINH | string | Einheit [grad] Grad |
| STAT_SUMMENLENKWINKEL_SENSOR_STATUS_WERT | int | Dieses Ergebnis gibt an, ob der Summenlenkwinkelsensor RAD kalibriert ist und ob der Sensor gueltig moegliche Faelle '-0' --&gt; Sensorwert ist nicht gueltig '-1' --&gt; Sensorwert ist gueltig '0-' --&gt; Sensor ist nicht kalibriert '1-' --&gt; Sensor ist kalibriert CAN-ID  : 195 / 0x0C3 Telegrammlaenge KWP, 1 Byte |
| STAT_SUMMENLENKWINKEL_SENSOR_STATUS_BIT0_TEXT | string | moegliche Faelle '-0' --&gt; Sensorwert ist nicht gueltig '-1' --&gt; Sensorwert ist gueltig Auswertung ueber Tabellenzugriff, --&gt; 'StatusLWGBit0' |
| STAT_SUMMENLENKWINKEL_SENSOR_STATUS_BIT1_TEXT | string | moegliche Faelle '0-' --&gt; Sensor ist nicht kalibriert '1-' --&gt; Sensor ist kalibriert Text zu Status Summenlenkwinkel Bit 0 Auswertung ueber Tabellenzufriff 'StatusLWGBit1' |
| STAT_SUMMENLENKWINKEL_SENSOR_CAN_ERROR_WERT | int | Fehlerstatus CAN Telegramm Summenlenkwinkel moegliche Faelle 0x00 --&gt; CAN Botschaft, i.o 0x02 --&gt; CAN Botschaft noch nie vorhanden gewesen, init 0x04 --&gt; CAN Botschaft, timeout 0x08 --&gt; CAN Botschaft Inhalt ungueltig 0x10 --&gt; CAN Botschaft ,Ueberpruefung der Nachricht fehlerhaft 0x20 --&gt; CAN Botschaft Sampling CAN-ID  : 195 / 0x0C3 Telegrammlaenge KWP, 1 Byte |
| STAT_SUMMENLENKWINKEL_SENSOR_CAN_ERROR_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; StatusCANFehler |
| STAT_SUMMENLENKWINKEL_SENSOR_ALIVECOUNTER_WERT | int | CAN-ID  : 195 / 0x0C3 Alivezaehler des Summenlenkwinkels (0..255) Telegrammlaenge KWP, 1 Byte |
| STAT_SUMMENLENKWINKEL_SENSOR_GUELTIGKEIT_SPANNUNGSVERSORUNG_WERT | int | moegliche Faelle 0x00 --&gt; Spannungsversorgung in Ordnung 0x01 --&gt; Spannungsversorgung zum Sensor (Kurzschluss Kabelbaum) und/oder Sensor NICHT in Ordnung moegliche Faelle Ueberwachung der Sensorversorgungssp. mittels ZFLS Fkt 'R_fdpDiagLws_xdb' Telegrammlaenge KWP, 1 Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-mpc-error-info"></a>
### STATUS_MPC_ERROR_INFO

Auslesen des MPC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $30 InputOutputLocalIdentifier(IOLI) $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_FEHLER | int | Anzahl der Fehler im Fehlerspeicher (2 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-fsp-mpc-controlfeld"></a>
### STATUS_FSP_MPC_CONTROLFELD

Auslesen des MPC Fehlerspeicher Diagnose Kontrollfeld ZFLS Konserve, ZFLS EXCEL Tabelle KWP2000: $30 InputOutputControlByLocalIdentifier $32 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | DTC Codes des INFO Fehlerspeicherbereiches, 2 Byte Wertebereich des DTC[6001..60FF] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DTCINFO_CODE_WERT | int | FehlerNr des INFO FSP Eintrages, ohne Prefix 60 |
| STAT_DTCINFO_CODE_TEXT | string | Fehlertext des INFO FSP Eintrages Zugriff auf Tabelle 'IOrtTexte' |
| STAT_CRTL1_HEX | string | Kontrollwort 1, 2 Byte |
| STAT_CRTL2_HEX | string | Kontrollwort 2, 2 Byte |
| STAT_VOR_HEX | string | Vorwaertsfilterung, 2 Byte |
| STAT_RUECK_HEX | string | Rueckwaertsfilterung, 2 Byte |
| STAT_UWBLOCK_HEX | string | Umweltbedblock, 1 Byte |
| STAT_START_BK_COUNT_HEX | string | interner ZF Zaehler |
| STAT_SUBFCT_LIMIT_HEX | string | Ersatzfunktion |
| STAT_SUBFCT_HEX | string | Ersatzfkt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-fsp-nec-controlfeld"></a>
### STATUS_FSP_NEC_CONTROLFELD

Auslesen des NEC Fehlerspeicher Diagnose Kontrollfeld ZFLS Konserve, ZFLS EXCEL Tabelle KWP2000: $30 InputOutputControlByLocalIdentifier $33 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | DTC Codes des INFO Fehlerspeicherbereiches, 2 Byte Wertebereich des DTC[6101..61FF] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DTCINFO_CODE_WERT | int | FehlerNr des INFO FSP Eintrages, ohne Prefix 61 |
| STAT_DTCINFO_CODE_TEXT | string | Fehlertext des INFO FSP Eintrages Zugriff auf Tabelle 'IOrtTexte' |
| STAT_SUBFCT_HEX | string | Ersatzfkt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-eco-strom-ma"></a>
### STEUERN_ECO_STROM_MA

Auslesen des MPC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $20 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ECO_STROM_SOLL_WERT | int | zu stellender Strom fuer das ECO Ventil, (2 Byte) Wertebereich[0..1000 mA] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECO_STROM_SOLL_R_WERT | int | zurueckglesener Soll-Strom fuer das ECO Ventil, (2 Byte) Wertebereich[0..1000 mA] |
| ECO_STROM_IST_WERT | int | zurueckglesener Ist-Strom fuer das ECO Ventil, (2 Byte) Wertebereich[0..1000 mA] |
| ECO_STROM_EINH | string | mA |
| ECO_STATUS_AKTUELL | int | (1 Byte) Wert '0', Strom konnte gestellt werden Wert '87', '88', Strom konnte NICHT gestellt werden |
| FAHRZEUG_GESCHWINDIGKEIT_WERT | real | korrigierte Fahrzeuggeschwindigkeit von ASCET 'MSG_R_Vx_corr', Laenge ( 4 Byte ) Telegrammuebertragung[m/s], Normierungsfaktor 1000 Skalierungsfaktor SGBD [km/h] = 3600/1E6 |
| FAHRZEUG_GESCHWINDIGKEIT_EINH | string | Einheit [km/h] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-servo-strom-ma"></a>
### STEUERN_SERVO_STROM_MA

Auslesen des MPC Fehlerspeichers KWP2000: $30 InputOutputControlByLocalIdentifier $21 InputOutputLocalIdentifier(IOLI) $07 InputOutputControlParameter(IOCP) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERVO_STROM_SOLL_WERT | int | zu stellender Strom fuer das Servo Ventil Wertebereich[0..1000 mA] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERVO_STROM_SOLL_R_WERT | int | zurueckglesener Soll-Strom fuer das Serco Ventil, (2 Byte) Wertebereich[0..1000 mA] |
| SERVO_STROM_IST_WERT | int | gestellender Strom fuer das Servo Ventil Wertebereich[0..1000 mA] |
| SERVO_STROM_EINH | string | mA |
| SERVO_STATUS_AKTUELL | int | Wert '0', Strom konnte gestellt werden Wert '87', '88', Strom konnte NICHT gestellt werden |
| FAHRZEUG_GESCHWINDIGKEIT_WERT | real | korrigierte Fahrzeuggeschwindigkeit von ASCET 'MSG_R_Vx_corr', Laenge ( 4 Byte ) Telegrammuebertragung[m/s], Normierungsfaktor 1000 Skalierungsfaktor SGBD [km/h] = 3600/1E6 |
| FAHRZEUG_GESCHWINDIGKEIT_EINH | string | Einheit [km/h] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-ecoservo"></a>
### STEUERN_ECOSERVO

KWP2000: $3B WriteDataByLocalIdentifier KWP2000: $91 SubID Freischaltung Bestromung der ECO SERVO Ventile ueber Diagnose

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_PSW | string | OKAY, wenn fehlerfrei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-eeprom-seriennummer-szl"></a>
### STATUS_EEPROM_SERIENNUMMER_SZL

Auslesen der im AFS EEPROM abgelegten Seriennummer des SZL AFS wird/bleibt inaktiv falls SZL getauscht wird KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdentifier(IOLI) $08 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEPROM_SERIENNUMMER_SZL_WERT | string | CAN-ID  : 200 / 0x0C8 8-stellige Seriennummer gesendet in HEX ( Laenge 4 Byte ) gesendet im MUX Verfahren bei wert '0' und '1' z.B.: '8765(1) 4321(0)' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-eeprom-offset-szl"></a>
### STATUS_EEPROM_OFFSET_SZL

Auslesen des im AFS EEPROM abgelegten Fahrerlenkwinkeloffsets vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier $02 InputOutputLocalIdentifier(IOLI) $08 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEPROM_FAHRER_LENKWINKEL_OFFSET_SZL_WERT | real | Fahrerlenkwinkeloffset vom SZL in Grad ueber F-CAN, Laenge ( 2 Byte ) CAN-ID, 200 / 0xC8 Achtung MULTIPLEX Botschaft Skalierungsfaktor (PH) = 0,04395 * (HEX)  [°/s] Skalierungsfaktor (PH)[km/h] = 180/4096 * (HEX) Ungueltigkeitsbez. 8000h |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit [Grad] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-eeprom-sensoren"></a>
### STATUS_EEPROM_SENSOREN

Sensordaten aus EEPROM lesen auch mit COTOOL32 KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdentifier(IOLI) $08 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEPROM_SENSOR_DATEN | binary | AdaptivDaten die aus dem EEPROM gelesen werden |
| STAT_GIERRATEN_1_OFFSET_WERT | real | abgelegter Gierratenoffset 1 im EEPROM Skalierungsfaktor 100000 Wertebereich -0,2....0,2 rad/s Telegramminterpretation (INTELFormat, LOWByte,HighByte), Laenge ( 2 Byte ) |
| STAT_GIERRATEN_2_OFFSET_WERT | real | abgelegter Gierratenoffset 2 im EEPROM Skalierungsfaktor 100000 Wertebereich -0,2....0,2 rad/s Telegramminterpretation (INTELFormat, LOWByte,HighByte), Laenge ( 2 Byte ) |
| STAT_GIERRATEN_OFFSET_EINH | string | Einheit [rad/s] |
| STAT_OUERBESCH_1_OFFSET_WERT | real | abgelegter Querbeschleunigungsoffset 1 im EEPROM Skalierungsfaktor 5000 Wertebereich -5....5 m/s2 Telegramminterpretation (INTELFormat, LOWByte,HighByte), Laenge ( 2 Byte ) |
| STAT_OUERBESCH_2_OFFSET_WERT | real | abgelegter Querbeschleunigungsoffset 2 im EEPROM Skalierungsfaktor 5000 Wertebereich -5....5 m/s2 Telegramminterpretation (INTELFormat, LOWByte,HighByte), Laenge ( 2 Byte ) |
| STAT_QUERBESCH_OFFSET_EINH | string | Einheit [m/s*s] |
| STAT_SUMMENLENKWINKEL_OFFSET_WERT | real | abgelegter Summenlenkwinkeloffset im EEPROM Skalierungsfaktor 10000 Wertebereich -0,3....3,0 rad Telegramminterpretation (INTELFormat, LOWByte,HighByte), Laenge ( 2 Byte ) |
| STAT_SUMMENLENKWINKEL_OFFSET_EINH | string | Einheit [rad] |
| STAT_GIERRATEN_EMPFINDLICHKEIT_1_WERT | real | abgelegte Gierratenempfindlichkeit 1 im EEPROM Skalierungsfaktor 20000 Wertebereich 0,8....1,2 % Telegramminterpretation (INTELFormat, LOWByte,HighByte), Laenge ( 2 Byte ) |
| STAT_GIERRATEN_EMPFINDLICHKEIT_2_WERT | real | abgelegte Gierratenempfindlichkeit 2 im EEPROM Skalierungsfaktor 20000 Wertebereich 0,8....1,2 % Telegramminterpretation (INTELFormat, LOWByte,HighByte), Laenge ( 2 Byte ) |
| JOB_STATUS | string | OKAY, ERROR_.. |
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

NUR Fehlerspeicher des MPC loeschen KWP2000: $14 ClearDiagnosticInformation $FF,$00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-fs-nec-loeschen"></a>
### FS_NEC_LOESCHEN

NUR Fehlerspeicher des NEC loeschen KWP2000: $14 ClearDiagnosticInformation $FF $01 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lwg-init"></a>
### START_LWG_INIT

Start der Summenlenkwinkelinitialisierung KWP2000: $31 StartRoutineByLocalIdentifier $50 RoutineLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| LWG_INIT_IO | int | ASCET/ASSET Variable ob Init LWG akzeptiert wurde |
| LWG_BIT_0 | int | ASCET/ASSET Variable ob Init LWG erfolgreich |
| ANZAHL_FKTAUFRUFE | int | Anzahl der SG internen Fkt.durchlaeufe |
| FAHRERLENKWINKEL_QUAL_ASCET | int | ASCET/ASSET Variable ob Fahrerlenkwinkel gueltig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-sensorcluster-offset-abgleich"></a>
### START_SENSORCLUSTER_OFFSET_ABGLEICH

AFS EEPROM Sensorclusteroffsetwerte mit DEFAULT Daten beschreiben KWP2000: $31 StartRoutineByLocalIdentifier $51 RoutineLocalIdentifier Modus  : SG darf NICHT im NORMAL_MODE, Fahrzeuggeschwindigkeit kleiner 5 km/h Modus  : Zugriff auf EEPROM muss moeglich sein Modus  : um die Werte ins EEPROM zu uebenehmen MUSS SG ueber POSTRUN laufen Modus  : Wechsel Klemme 15

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSORCLUSTER_OFFSET_ABGLEICH_WERT | int | Variable, '1' Abgleich aktiv Variable, '0' Abgleich deaktiviert Wertebereich [0,1] Abgleich fuer Gierratenoffsetwerte 1,2 Querbeschleunigungsoffsetwerte 1,2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-summenlenkwinkel-offset-abgleich"></a>
### START_SUMMENLENKWINKEL_OFFSET_ABGLEICH

AFS EEPROM Summenlenkwinkeloffsetwerte mit DEFAULT Daten beschreiben KWP2000: $31 StartRoutineByLocalIdentifier $52 RoutineLocalIdentifier Modus  : SG darf NICHT im NORMAL_MODE, Fahrzeuggeschwindigkeit kleiner 5 km/h Modus  : Zugriff auf EEPROM muss moeglich sein Modus  : um die Werte ins EEPROM zu uebenehmen MUSS SG ueber POSTRUN laufen Modus  : Wechsel Klemme 15

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SUMMENLENKWINKEL_OFFSET_ABGLEICH_WERT | int | Variable, '1' Abgleich aktiv Variable, '0' Abgleich deaktiviert Wertebereich [0,1] Abgleich fuer Summenlenkwinkeloffsetwert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-gierratenempfindlichkeit-abgleich"></a>
### START_GIERRATENEMPFINDLICHKEIT_ABGLEICH

AFS EEPROM Gierratenempfindlichkeiten mit DEFAULT Daten beschreiben KWP2000: $31 StartRoutineByLocalIdentifier $53 RoutineLocalIdentifier Modus  : SG darf NICHT im NORMAL_MODE, Fahrzeuggeschwindigkeit kleiner 5 km/h Modus  : Zugriff auf EEPROM muss moeglich sein Modus  : um die Werte ins EEPROM zu uebenehmen MUSS SG ueber POSTRUN laufen Modus  : Wechsel Klemme 15

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GIERRATENEMPFINDLICHKEIT_ABGLEICH_WERT | int | Variable, '1' Abgleich aktiv Variable, '0' Abgleich deaktiviert Wertebereich [0,1] Abgleich fuer Gierratenempfindlichkeitswerte 1,2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lwm-ruecksetzen"></a>
### START_LWM_RUECKSETZEN

1 Telegramm Motorlagewinkels auf ungueltig setzen, durch SG RESET Positive Antwort NUR im PRE_DRIVE und NORMAL_MODE 2 Telegramm Status des Motorlagewinkels wird ausgelesen KWP2000: $31 RequestRoutineResultsByLocalIdentifier $54 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GUELTIGKEIT_MOTORLAGEWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; NICHT gueltig ) moegliche Zustaende ( 1 --&gt; gueltig ) moegliche Zustaende ( 2 --&gt; nicht definiert ) |
| GUELTIGKEIT_MOTORLAGEWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| GUELTIGKEIT_MOTORLAGEWINKEL_WERT | int | moegliche Zustaende ( 0 --&gt; NICHT gueltig ) moegliche Zustaende ( 1 --&gt; gueltig ) moegliche Zustaende ( 2 --&gt; nicht definiert ) |
| GUELTIGKEIT_MOTORLAGEWINKEL_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; EinAus  ( 1 Byte ) |
| INBETRIEBNAHME_LWG_FERTIG | int | 0, wenn Inbetriebnahme NICHT erfolgreich 1, wenn Inbetriebnahme erfolgreich 2, nicht definiert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-lwg-quadrant-abfragen"></a>
### STATUS_LWG_QUADRANT_ABFRAGEN

Quadrantengueltigkeit des Summenlenkwinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $51 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LWG_QUALIFIER_WERT | int | 0, gueltiger Quadrant 1, ungueltiger Quadrant ASCET Qualifier 'MSG_I_LwG_qual'( 1 Byte ), verUNDET mit Maske 0x01 ausgewertet wird nur Bit '0' |
| STAT_LWG_QUALIFIER_TEXT | string | 0, gueltiger Quadrant 1, ungueltiger Quadrant ausgewertet in Tabelle 'LWGQuadrant' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-nec-flash-programmier-status-lesen"></a>
### NEC_FLASH_PROGRAMMIER_STATUS_LESEN

Zustand des NEC beim bzw. nach dem Flashen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $52 Resultat anfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NEC_FLASH_WERT | int | moegliche Zustaende ( 0 --&gt; FLASH_BOOT ) moegliche Zustaende ( 1 --&gt; FLASH_DRIVE ) moegliche Zustaende ( 2 --&gt; FLASH_BBIND ) moegliche Zustaende ( 3 --&gt; FLASH_NOT ) moegliche Zustaende ( 4 --&gt; FLASH_UNDEF ) |
| STAT_NEC_FLASH_TEXT | string | Textausgabe ueber Tabellenzugriff, --&gt; NecFlash  ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-adaptivdaten-abgleich-abfragen"></a>
### STATUS_ADAPTIVDATEN_ABGLEICH_ABFRAGEN

aktueller Zustand des EEPROM Adaptivdatenabgleichs KWP2000: $33 RequestRoutineResultsByLocalIdentifier $53 RoutineLocalIdentifier ( RELI ) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSORCLUSTER_OFFSET_ABGLEICH_WERT | int | Variable, '1' Abgleich aktiv Variable, '0' Abgleich deaktiviert Wertebereich [0,1] aktueller Status Abgleich fuer Gierratenoffsetwerte 1,2 Querbeschleunigungsoffsetwerte 1,2 |
| STAT_SUMMENLENKWINKEL_OFFSET_ABGLEICH_WERT | int | Variable, '1' Abgleich aktiv Variable, '0' Abgleich deaktiviert Wertebereich [0,1] aktueller Status Abgleich fuer Summenlenkwinkeloffsetwert |
| STAT_GIERRATENEMPFINDLICHKEIT_ABGLEICH_WERT | int | Variable, '1' Abgleich aktiv Variable, '0' Abgleich deaktiviert Wertebereich [0,1] aktueller Status Gierratenempfindlichkeitswerte 1,2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: 'JobResult' |
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

<a id="job-zf-factory-daten-lesen"></a>
### ZF_FACTORY_DATEN_LESEN

MPC EEPROM Daten lesen fuer INPA Darstellung KWP2000: $23 readMemoryByAddress,(RMBA) MemoryTypeIdentifier,ROMX = 2 gueltige MPC Speicher Adressen: 0x0200-0x0FFF EEPROM Speichergroesse 4096 Byte maximale DPRAM Uebertragungsbreite 128 Byte maximale Aufrufbreite fuer ZFLS Fkt. 16 Byte hier werden 12 Byte aus dem Werksdatenbereich ausgelesen, ab Adresse  0x0FCA Modus  : Default

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

<a id="job-status-afs-os-unter-nummer"></a>
### STATUS_AFS_OS_UNTER_NUMMER

Auslesen verschiedener Betriebssystem (OS,SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID    $32 InputOutputLocalIdentifier(IOLI) SubID    $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEM_PROG | int | aktueller Systemstatus des NEC |
| STAT_SYSTEM_DATEN | int | gewuenschter Status des MPC gueltige Werte 0 bis ? |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (11 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (61 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (4 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (6 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (125 × 9)
- [HORTTEXTE](#table-horttexte) (60 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (6 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (125 × 9)
- [HARTTEXTEERWEITERT](#table-harttexteerweitert) (4 × 3)
- [IORTTEXTE](#table-iorttexte) (108 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (19 × 9)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (8 × 3)
- [LOWLEVEL](#table-lowlevel) (1 × 3)
- [SYSTEMSTATE](#table-systemstate) (1 × 10)
- [ERRORSTATE](#table-errorstate) (1 × 33)
- [DPSI](#table-dpsi) (1 × 17)
- [DEH](#table-deh) (1 × 17)
- [LWS](#table-lws) (1 × 17)
- [MDYN](#table-mdyn) (1 × 17)
- [PROZESSORSTATI](#table-prozessorstati) (8 × 2)
- [CURRENTOPMODESTATI](#table-currentopmodestati) (5 × 2)
- [DPRAMSTATI](#table-dpramstati) (4 × 2)
- [EINAUS](#table-einaus) (3 × 2)
- [GUEROTOR](#table-guerotor) (4 × 2)
- [BITFKTAFS](#table-bitfktafs) (8 × 4)
- [STATUSCANFEHLER](#table-statuscanfehler) (7 × 2)
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
- [NECFEHLERCODE](#table-necfehlercode) (41 × 3)
- [NECFEHLERTYP](#table-necfehlertyp) (91 × 3)
- [AUSEIN](#table-ausein) (3 × 2)
- [SPERRE](#table-sperre) (7 × 2)
- [MPCREV](#table-mpcrev) (2 × 2)
- [BITGMKAFS](#table-bitgmkafs) (5 × 2)
- [GMKQUALBIT0](#table-gmkqualbit0) (3 × 2)
- [GMKQUALBIT1](#table-gmkqualbit1) (3 × 2)
- [GMKQUALBIT2](#table-gmkqualbit2) (3 × 2)
- [GMKQUALBIT3](#table-gmkqualbit3) (3 × 2)
- [GMKQUALBIT4](#table-gmkqualbit4) (3 × 2)
- [GMKQUALBIT5](#table-gmkqualbit5) (3 × 2)
- [LWGQUADRANT](#table-lwgquadrant) (3 × 2)
- [SZLPROZINFO](#table-szlprozinfo) (3 × 2)
- [GMK](#table-gmk) (1 × 17)
- [GMKQUALBIT6](#table-gmkqualbit6) (3 × 2)
- [GMKQUALBIT7](#table-gmkqualbit7) (3 × 2)
- [INFO_A](#table-info-a) (1 × 6)
- [INFO_B](#table-info-b) (1 × 12)
- [INFO_C](#table-info-c) (1 × 2)
- [INFO_D](#table-info-d) (1 × 2)
- [MDYQUALBIT0](#table-mdyqualbit0) (3 × 2)
- [MDYQUALBIT1](#table-mdyqualbit1) (3 × 2)
- [LWDSQUALBIT0](#table-lwdsqualbit0) (3 × 2)
- [LWDSQUALBIT1](#table-lwdsqualbit1) (3 × 2)
- [LWDSQUALBIT2](#table-lwdsqualbit2) (3 × 2)
- [LWDSQUALBIT3](#table-lwdsqualbit3) (3 × 2)
- [LWDSQUALBIT4](#table-lwdsqualbit4) (3 × 2)
- [LWGQUALBIT0](#table-lwgqualbit0) (3 × 2)
- [LWGQUALBIT1](#table-lwgqualbit1) (3 × 2)
- [LWGQUALBIT2](#table-lwgqualbit2) (3 × 2)
- [LWGQUALBIT3](#table-lwgqualbit3) (3 × 2)
- [LWGQUALBIT4](#table-lwgqualbit4) (3 × 2)
- [LWGQUALBIT5](#table-lwgqualbit5) (3 × 2)
- [LWGQUALBIT6](#table-lwgqualbit6) (3 × 2)
- [REFVXQUALBIT0](#table-refvxqualbit0) (3 × 2)
- [REFVXQUALBIT1](#table-refvxqualbit1) (3 × 2)
- [REFVXQUALBIT2](#table-refvxqualbit2) (3 × 2)
- [REFVXQUALBIT3](#table-refvxqualbit3) (3 × 2)
- [AYQUALBIT0](#table-ayqualbit0) (3 × 2)
- [AYQUALBIT1](#table-ayqualbit1) (3 × 2)
- [AYQUALBIT2](#table-ayqualbit2) (3 × 2)
- [AYQUALBIT4](#table-ayqualbit4) (3 × 2)
- [AYQUALBIT5](#table-ayqualbit5) (3 × 2)
- [RRQUALBIT0](#table-rrqualbit0) (3 × 2)
- [RRQUALBIT1](#table-rrqualbit1) (3 × 2)
- [RRQUALBIT2](#table-rrqualbit2) (3 × 2)
- [RRQUALBIT3](#table-rrqualbit3) (3 × 2)
- [RRQUALBIT4](#table-rrqualbit4) (3 × 2)
- [RRQUALBIT5](#table-rrqualbit5) (3 × 2)
- [BMWMODE](#table-bmwmode) (7 × 2)
- [FERTIG](#table-fertig) (3 × 2)
- [DXJOB](#table-dxjob) (23 × 2)
- [DXSTATUS](#table-dxstatus) (20 × 2)
- [STATUSLWGBIT0](#table-statuslwgbit0) (3 × 2)
- [STATUSLWGBIT1](#table-statuslwgbit1) (3 × 2)

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

Dimensions: 81 rows × 2 columns

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
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
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

Dimensions: 61 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x612C | Hardwarefehler Steuergerät |
| 0x612D | Giermomentenkompensations Fehler |
| 0x612E | Fahrgestellnummernvergleich |
| 0x612F | Codierdatenfehler |
| 0x6130 | Boot- oder Flashfehler MPC |
| 0x6131 | Flashvorgang oder Flashfehler NEC |
| 0x6132 | kein 2 Prozessor SZL gefunden oder verbaut |
| 0x6133 | Motorspannung |
| 0x6134 | Motorstrom |
| 0x6135 | SZL neu verbaut oder neu abgeglichen |
| 0x6136 | Sensorversorgung Motorlage und -position |
| 0x6137 | Motorlagesensor |
| 0x6138 | Motor-uebertemperatur |
| 0x6139 | Fzg Ref. Geschw. oder Fahrtrichtung unsicher oder nicht verfuegbar |
| 0x613A | Versorgungsspannung Kl. 30 (&lt; 7.5 Volt) |
| 0x613B | Fahrdynamiksensoren |
| 0x613C | Winkelsummenbeziehung fehlerhaft |
| 0x613D | elektr. Sperrenfehler |
| 0x613E | mechanischer Sperrenfehler |
| 0x613F | Plausibilitaet Lenkwinkel-Rad (Summenlenkwinkel) |
| 0x6140 | Redundanzvergleich Fahrerlenkwinkel oben |
| 0x6141 | Motordynamikueberwachung |
| 0x6142 | ECO-Ventil |
| 0x6143 | SERVO-Ventil |
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
| 0xCE93 | Botschaft (Lenkradwinkel oben, ID=0C9)Initialisierungsphase |
| 0xCE94 | Botschaft (Fahrdynamiksensor 1, ID=0CD) vom F-CAN |
| 0xCE95 | Botschaft (Fahrdynamiksensor 2, ID=0D1) vom F-CAN |
| 0xCE96 | Botschaft (Radgeschwindigkeiten, ID=0CE) vom DSC F-CAN |
| 0xCE97 | Botschaft (Lenkwinkel-Rad (Summenlenkwinkel), ID=0C3) vom F-CAN |
| 0xCE98 | Botschaft (Regeleingriffe DSC_AFS, ID=11E) vom DSC F-CAN |
| 0xCE99 | Botschaft (Lenkradwinkel oben, ID=0C9) vom SZL F-CAN |
| 0xCE9C | Botschaft (Status DSC, ID=19E) vom DSC PT-CAN |
| 0xCE9D | Botschaft (Motormoment 1, ID=0A8) vom DME PT-CAN |
| 0xCE9E | Botschaft (Motormoment 3, ID=0AA) vom DME PT-CAN |
| 0xCE9F | Botschaft (Motordaten, ID=1D0) vom DME PT-CAN |
| 0xCEA0 | Botschaft (Motor-Start-Stop Automatik, ID=308) vom DME PT-CAN |
| 0xCEA1 | Botschaft (Klemmenstatus, ID=130) vom CAS PT-CAN |
| 0xCEA3 | Botschaft (Kilometerstand, ID=330) vom KombiInstr. PT-CAN |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00000011 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxx00 | 100 | Allgemeiner Fehler |
| xxxxxx01 | 101 | FSP uebergelaufen |
| xxxxxx10 | 110 | FSP nicht uebergelaufen |
| xxxxxx11 | 111 | Status ungueltig |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 6 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x612D | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | GMK |
| 0x613B | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DPSI |
| 0x613F | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DEH |
| 0x6140 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | LWS |
| 0x6141 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | MDYN |
| default | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | 0xFF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 125 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Reihenfolge der Ablage | - | -- | unsigned char | - | - | - | - |
| 0x02 | ZF-LS Fehlercode | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | ZF-LS Fehlerart | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | -- | signed char | -- | 2 | 1 | 0 |
| 0x05 | Querbeschleunigung | m/(s*s) | -- | signed char | -- | 1 | 7 | 0 |
| 0x06 | Gierrate | rad/s | -- | signed char | -- | 1 | 70 | 0 |
| 0x07 | Summenlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x08 | Fahrerlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x09 | Versorgungsspannung | Volt | -- | unsigned char | -- | 1 | 12.75 | 0 |
| 0x0A | ohne Bedeutung | ? | -- | signed char | -- | 1 | 1 | 0 |
| 0x0B | diverse SG-Stati | digital | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x10 | Abschaltung der Aktivlenkung Bit 0 | 0/1 | -- | 0x00000001 | -- | - | - | - |
| 0x11 | Abschaltung der Gierratenregelung Bit 1 | 0/1 | -- | 0x00000002 | -- | - | - | - |
| 0x12 | Ersatzwert fuer Motordrehzahl fuer ECO-Funktionalitaet Bit 2 | 0/1 | -- | 0x00000004 | -- | - | - | - |
| 0x13 | Einfrieren oder langsames Zurueckstellen des aktuellen Motorlagewinkels  Bit 3 | 0/1 | -- | 0x00000008 | -- | - | - | - |
| 0x14 | Sofortige Abschaltung der GRR Bit 4 | 0/1 | -- | 0x00000010 | -- | - | - | - |
| 0x15 | Verzoegerte Abschaltung der GRR Bit 5 | 0/1 | -- | 0x00000020 | -- | - | - | - |
| 0x16 | Einfrieren der Lenkuebersetzung(aktueller Zuendungszyklus) Bit 6 | 0/1 | -- | 0x00000040 | -- | - | - | - |
| 0x17 | Einfrieren der geschwindigkeitsabhaengigen Lenkuebersetzung Bit 7 | 0/1 | -- | 0x00000080 | -- | - | - | - |
| 0x18 | Einfrieren der Fahrtrichtung Bit 8 | 0/1 | -- | 0x00000100 | -- | - | - | - |
| 0x19 | Ersatzwert fuer Gierrate fuer die Fkt.en Servotro. u. DME Bit 9 | 0/1 | -- | 0x00000200 | -- | - | - | - |
| 0x1A | Ersatzwert fuer Querbesch. fuer die Fkt.en Servotro. u. DME Bit 10 | 0/1 | -- | 0x00000400 | -- | - | - | - |
| 0x1B | Ersatzwert fuer Lenkwinkelgeschw. fuer die Fkt.en Servotro. u. DME Bit 11 | 0/1 | -- | 0x00000800 | -- | - | - | - |
| 0x1C | Fehler des Fahrerlenkwinkels oder des Motorlagewinkels Bit 12 | 0/1 | -- | 0x00001000 | -- | - | - | - |
| 0x1D | konst. Ersatzwert fuer den Summenlenkwinkel Bit 13 | 0/1 | -- | 0x00002000 | -- | - | - | - |
| 0x1E | Fehler des Summenlenkwinkels oder des Motorlagewinkels Bit 14 | 0/1 | -- | 0x00004000 | -- | - | - | - |
| 0x1F | konst. Ersatzwert fuer den Fahrerlenkwinkel Bit 15 | 0/1 | -- | 0x00008000 | -- | - | - | - |
| 0x20 | reversible GMK Abschaltung Bit 16 | 0/1 | -- | 0x00010000 | -- | - | - | - |
| 0x21 | irreversible GMK Abschaltung Bit 17 | 0/1 | -- | 0x00020000 | -- | - | - | - |
| 0x22 | Ersatzwert des Motormoments fuer SNK Bit 18 | 0/1 | -- | 0x00040000 | -- | - | - | - |
| 0x23 | Ersatzmassnahme unbenutzt Bit 19 | 0/1 | -- | 0x00080000 | -- | - | - | - |
| 0x24 | Ersatzmassnahme unbenutzt Bit 20 | 0/1 | -- | 0x00100000 | -- | - | - | - |
| 0x25 | Ersatzmassnahme unbenutzt Bit 21 | 0/1 | -- | 0x00200000 | -- | - | - | - |
| 0x26 | Ersatzmassnahme unbenutzt Bit 22 | 0/1 | -- | 0x00400000 | -- | - | - | - |
| 0x27 | Ersatzmassnahme unbenutzt Bit 23 | 0/1 | -- | 0x00800000 | -- | - | - | - |
| 0x28 | Ersatzmassnahme unbenutzt Bit 24 | 0/1 | -- | 0x01000000 | -- | - | - | - |
| 0x29 | Ersatzmassnahme unbenutzt Bit 25 | 0/1 | -- | 0x02000000 | -- | - | - | - |
| 0x2A | Ersatzmassnahme unbenutzt Bit 26 | 0/1 | -- | 0x04000000 | -- | - | - | - |
| 0x2B | Ersatzmassnahme unbenutzt Bit 27 | 0/1 | -- | 0x08000000 | -- | - | - | - |
| 0x2C | Ersatzmassnahme unbenutzt Bit 28 | 0/1 | -- | 0x10000000 | -- | - | - | - |
| 0x2D | Ersatzmassnahme unbenutzt Bit 29 | 0/1 | -- | 0x20000000 | -- | - | - | - |
| 0x2E | Ersatzmassnahme unbenutzt Bit 30 | 0/1 | -- | 0x40000000 | -- | - | - | - |
| 0x2F | Ersatzmassnahme unbenutzt Bit 31 | 0/1 | -- | 0x80000000 | -- | - | - | - |
| 0x30 | Sensorfehler FDYS Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x31 | Gradient Fehlerverdacht FDYS Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x32 | Gradient Fehler FDYS Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x33 | Signal Peak Fehler FDYS Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x34 | Offsetueberwachung Fehler FDYS Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x35 | Empfindlichkeits Ueberwachung Fehler FDYS Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x36 | Roh-Redundanz Fehlerverdacht FDYS Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x37 | Roh-Redundanz Fehler FDYS Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x38 | unbenutzt FDYS Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x39 | Referenz Redundanz Fehlerverdacht FDYS Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x3A | Referenz Redundanz Fehler FDYS Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x3B | unbenutzt FDYS Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x3C | Fehler im Sensorcluster 1 FDYS Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x3D | Fehler im Sensorcluster 2 FDYS Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x3E | unbenutzt FDYS Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x3F | unbenutzt FDYS Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x40 | Lenkwinkelgradient Fehlerverdacht LWG Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x41 | Lenkwinkelgradient Fehler LWG Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x42 | Lenkwinkel Peak Fehler LWG Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x43 | unbenutzt LWG Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x44 | Lenkwinkeloffset Fehlerverdacht LWG Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x45 | Lenkwinkeloffset Fehler LWG Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x46 | Winkelsummengleichung Fehlerverdacht LWG Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x47 | Winkelsummengleichung Fehler LWG Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x48 | unbenutzt LWG Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x49 | unbenutzt LWG Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x4A | unbenutzt LWG Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x4B | unbenutzt LWG Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x4C | unbenutzt LWG Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x4D | unbenutzt LWG Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x4E | unbenutzt LWG Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x4F | unbenutzt LWG Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x50 | Can Signal Fehlerwert des Maincontrollers SZL LWDS Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x51 | Can Signal Fehlerwert des Subcontrollers SZL LWDS Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x52 | Can Signal Timeout des Maincontrollers SZL LWDS Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x53 | Can Signal Timeout des Subcontrollers SZL LWDS Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x54 | Can Signal SZL in diesem Zündungszyklus nie dagewesen LWDS Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x55 | SZL Winkel außerhalb erwartetem Band LWDS Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x56 | Differenz zwischen redundaten Lenkwinkelsignalen ist zu groß LWDS Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x57 | Differenz nach Timeout zwischen aufeinanderfolgenden Signalwerten zu groß LWSD Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x58 | Kein 2uC SZL LWDS Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x59 | SZL neu verbaut oder neu abgeglichen LWDS Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x5A | SZL Typ wurde nicht empfangen LWDS Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x5B | unbenutzt LWDS Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x5C | unbenutzt LWDS Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x5D | unbenutzt LWDS Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x5E | unbenutzt LWDS Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x5F | unbenutzt LWDS Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x60 | Fehler Integral 1 MDYN Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x61 | Fehler Integral 2 MDYN Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x62 | unbenutzt MDYN Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x63 | unbenutzt MDYN Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x64 | unbenutzt MDYN Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x65 | unbenutzt MDYN Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x66 | unbenutzt MDYN Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x67 | unbenutzt MDYN Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x68 | unbenutzt MDYN Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x69 | unbenutzt MDYN Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x6A | unbenutzt MDYN Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x6B | unbenutzt MDYN Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x6C | unbenutzt MDYN Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x6D | unbenutzt MDYN Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x6E | unbenutzt MDYN Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x6F | unbenutzt MDYN Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x70 | GMK keine Lenkanforderung Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x71 | GMK Lenkanforderung Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x72 | GMK irreversibel deaktiviert Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x73 | GMK Timeout Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x74 | GMK Fehlerwert Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x75 | GMK CRC/Alive Fehler Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x76 | GMK Teilsollwert zu hoch Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x77 | GMK Regelung zu lang Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x78 | GMK Teilsollwert ins Modell ungleich NULL Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x79 | DSC Status passiv Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x7A | DSC Status defekt Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x7B | DSC Status DTC Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x7C | unbenutzt GMK Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x7D | ECO Status Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x7E | Motordynamik SW1 Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x7F | Signalfehler AY,RR Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0xFF | ohne Bedeutung | 1 | -- | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 60 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x612C | Hardwarefehler Steuergerät |
| 0x612D | Giermomentenkompensations Fehler |
| 0x612E | Fahrgestellnummernvergleich |
| 0x612F | Codierdatenfehler |
| 0x6130 | Boot- oder Flashfehler MPC |
| 0x6131 | Flashvorgang oder Flashfehler NEC |
| 0x6132 | kein 2 Prozessor SZL gefunden oder verbaut |
| 0x6133 | Motorspannung |
| 0x6134 | Motorstrom |
| 0x6135 | SZL neu verbaut oder neu abgeglichen |
| 0x6136 | Sensorversorgung Motorlage und -position |
| 0x6137 | Motorlagesensor |
| 0x6138 | Motor-uebertemperatur |
| 0x6139 | Fzg Ref. Geschw. oder Fahrtrichtung unsicher oder nicht verfuegbar |
| 0x613A | Versorgungsspannung Kl. 30 (&lt; 7.5 Volt) |
| 0x613B | Fahrdynamiksensoren |
| 0x613C | Winkelsummenbeziehung fehlerhaft |
| 0x613D | elektr. Sperrenfehler |
| 0x613E | mechanischer Sperrenfehler |
| 0x613F | Plausibilitaet Lenkwinkel-Rad (Summenlenkwinkel) |
| 0x6140 | Redundanzvergleich Fahrerlenkwinkel oben |
| 0x6141 | Motordynamikueberwachung |
| 0x6142 | ECO-Ventil |
| 0x6144 | Selbsthemmungsueberwachung |
| 0x6143 | SERVO-Ventil |
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
| 0xCE93 | Botschaft (Lenkradwinkel oben, ID=0C9)Initialisierungsphase |
| 0xCE94 | Botschaft (Fahrdynamiksensor 1, ID=0CD) vom F-CAN |
| 0xCE95 | Botschaft (Fahrdynamiksensor 2, ID=0D1) vom F-CAN |
| 0xCE96 | Botschaft (Radgeschwindigkeiten, ID=0CE) vom DSC F-CAN |
| 0xCE97 | Botschaft (Lenkwinkel-Rad (Summenlenkwinkel), ID=0C3) vom F-CAN |
| 0xCE98 | Botschaft (Regeleingriffe DSC_AFS, ID=11E) vom DSC F-CAN |
| 0xCE99 | Botschaft (Lenkradwinkel oben, ID=0C9) vom SZL F-CAN |
| 0xCE9C | Botschaft (Status DSC, ID=19E) vom DSC PT-CAN |
| 0xCE9D | Botschaft (Motormoment 1, ID=0A8) vom DME PT-CAN |
| 0xCE9E | Botschaft (Motormoment 3, ID=0AA) vom DME PT-CAN |
| 0xCE9F | Botschaft (Motordaten, ID=1D0) vom DME PT-CAN |
| 0xCEA1 | Botschaft (Klemmenstatus, ID=130) vom CAS PT-CAN |
| 0xCEA3 | Botschaft (Kilometerstand, ID=330) vom KombiInstr. PT-CAN |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00000011 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 6 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x612D | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | GMK |
| 0x613B | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DPSI |
| 0x613F | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | DEH |
| 0x6140 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | LWS |
| 0x6141 | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | MDYN |
| default | LOWLEVEL | SYSTEMSTATE | ERRORSTATE | 0xFF |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 125 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Reihenfolge der Ablage | - | -- | unsigned char | - | - | - | - |
| 0x02 | ZF-LS Fehlercode | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | ZF-LS Fehlerart | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | -- | signed char | -- | 2 | 1 | 0 |
| 0x05 | Querbeschleunigung | m/(s*s) | -- | signed char | -- | 1 | 7 | 0 |
| 0x06 | Gierrate | rad/s | -- | signed char | -- | 1 | 70 | 0 |
| 0x07 | Summenlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x08 | Fahrerlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x09 | Versorgungsspannung | Volt | -- | unsigned char | -- | 1 | 12.75 | 0 |
| 0x0A | ohne Bedeutung | ? | -- | signed char | -- | 1 | 1 | 0 |
| 0x0B | diverse SG-Stati | digital | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x10 | Abschaltung der Aktivlenkung Bit 0 | 0/1 | -- | 0x00000001 | -- | - | - | - |
| 0x11 | Abschaltung der Gierratenregelung Bit 1 | 0/1 | -- | 0x00000002 | -- | - | - | - |
| 0x12 | Ersatzwert fuer Motordrehzahl fuer ECO-Funktionalitaet Bit 2 | 0/1 | -- | 0x00000004 | -- | - | - | - |
| 0x13 | Einfrieren oder langsames Zurueckstellen des aktuellen Motorlagewinkels  Bit 3 | 0/1 | -- | 0x00000008 | -- | - | - | - |
| 0x14 | Sofortige Abschaltung der GRR Bit 4 | 0/1 | -- | 0x00000010 | -- | - | - | - |
| 0x15 | Verzoegerte Abschaltung der GRR Bit 5 | 0/1 | -- | 0x00000020 | -- | - | - | - |
| 0x16 | Einfrieren der Lenkuebersetzung(aktueller Zuendungszyklus) Bit 6 | 0/1 | -- | 0x00000040 | -- | - | - | - |
| 0x17 | Einfrieren der geschwindigkeitsabhaengigen Lenkuebersetzung Bit 7 | 0/1 | -- | 0x00000080 | -- | - | - | - |
| 0x18 | Einfrieren der Fahrtrichtung Bit 8 | 0/1 | -- | 0x00000100 | -- | - | - | - |
| 0x19 | Ersatzwert fuer Gierrate fuer die Fkt.en Servotro. u. DME Bit 9 | 0/1 | -- | 0x00000200 | -- | - | - | - |
| 0x1A | Ersatzwert fuer Querbesch. fuer die Fkt.en Servotro. u. DME Bit 10 | 0/1 | -- | 0x00000400 | -- | - | - | - |
| 0x1B | Ersatzwert fuer Lenkwinkelgeschw. fuer die Fkt.en Servotro. u. DME Bit 11 | 0/1 | -- | 0x00000800 | -- | - | - | - |
| 0x1C | Fehler des Fahrerlenkwinkels oder des Motorlagewinkels Bit 12 | 0/1 | -- | 0x00001000 | -- | - | - | - |
| 0x1D | konst. Ersatzwert fuer den Summenlenkwinkel Bit 13 | 0/1 | -- | 0x00002000 | -- | - | - | - |
| 0x1E | Fehler des Summenlenkwinkels oder des Motorlagewinkels Bit 14 | 0/1 | -- | 0x00004000 | -- | - | - | - |
| 0x1F | konst. Ersatzwert fuer den Fahrerlenkwinkel Bit 15 | 0/1 | -- | 0x00008000 | -- | - | - | - |
| 0x20 | reversible GMK Abschaltung Bit 16 | 0/1 | -- | 0x00010000 | -- | - | - | - |
| 0x21 | irreversible GMK Abschaltung Bit 17 | 0/1 | -- | 0x00020000 | -- | - | - | - |
| 0x22 | Ersatzwert des Motormoments fuer SNK Bit 18 | 0/1 | -- | 0x00040000 | -- | - | - | - |
| 0x23 | Ersatzmassnahme unbenutzt Bit 19 | 0/1 | -- | 0x00080000 | -- | - | - | - |
| 0x24 | Ersatzmassnahme unbenutzt Bit 20 | 0/1 | -- | 0x00100000 | -- | - | - | - |
| 0x25 | Ersatzmassnahme unbenutzt Bit 21 | 0/1 | -- | 0x00200000 | -- | - | - | - |
| 0x26 | Ersatzmassnahme unbenutzt Bit 22 | 0/1 | -- | 0x00400000 | -- | - | - | - |
| 0x27 | Ersatzmassnahme unbenutzt Bit 23 | 0/1 | -- | 0x00800000 | -- | - | - | - |
| 0x28 | Ersatzmassnahme unbenutzt Bit 24 | 0/1 | -- | 0x01000000 | -- | - | - | - |
| 0x29 | Ersatzmassnahme unbenutzt Bit 25 | 0/1 | -- | 0x02000000 | -- | - | - | - |
| 0x2A | Ersatzmassnahme unbenutzt Bit 26 | 0/1 | -- | 0x04000000 | -- | - | - | - |
| 0x2B | Ersatzmassnahme unbenutzt Bit 27 | 0/1 | -- | 0x08000000 | -- | - | - | - |
| 0x2C | Ersatzmassnahme unbenutzt Bit 28 | 0/1 | -- | 0x10000000 | -- | - | - | - |
| 0x2D | Ersatzmassnahme unbenutzt Bit 29 | 0/1 | -- | 0x20000000 | -- | - | - | - |
| 0x2E | Ersatzmassnahme unbenutzt Bit 30 | 0/1 | -- | 0x40000000 | -- | - | - | - |
| 0x2F | Ersatzmassnahme unbenutzt Bit 31 | 0/1 | -- | 0x80000000 | -- | - | - | - |
| 0x30 | Sensorfehler FDYS Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x31 | Gradient Fehlerverdacht FDYS Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x32 | Gradient Fehler FDYS Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x33 | Signal Peak Fehler FDYS Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x34 | Offsetueberwachung Fehler FDYS Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x35 | Empfindlichkeits Ueberwachung Fehler FDYS Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x36 | Roh-Redundanz Fehlerverdacht FDYS Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x37 | Roh-Redundanz Fehler FDYS Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x38 | unbenutzt FDYS Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x39 | Referenz Redundanz Fehlerverdacht FDYS Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x3A | Referenz Redundanz Fehler FDYS Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x3B | unbenutzt FDYS Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x3C | Fehler im Sensorcluster 1 FDYS Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x3D | Fehler im Sensorcluster 2 FDYS Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x3E | unbenutzt FDYS Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x3F | unbenutzt FDYS Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x40 | Lenkwinkelgradient Fehlerverdacht LWG Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x41 | Lenkwinkelgradient Fehler LWG Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x42 | Lenkwinkel Peak Fehler LWG Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x43 | unbenutzt LWG Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x44 | Lenkwinkeloffset Fehlerverdacht LWG Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x45 | Lenkwinkeloffset Fehler LWG Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x46 | Winkelsummengleichung Fehlerverdacht LWG Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x47 | Winkelsummengleichung Fehler LWG Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x48 | unbenutzt LWG Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x49 | unbenutzt LWG Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x4A | unbenutzt LWG Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x4B | unbenutzt LWG Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x4C | unbenutzt LWG Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x4D | unbenutzt LWG Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x4E | unbenutzt LWG Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x4F | unbenutzt LWG Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x50 | Can Signal Fehlerwert des Maincontrollers SZL LWDS Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x51 | Can Signal Fehlerwert des Subcontrollers SZL LWDS Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x52 | Can Signal Timeout des Maincontrollers SZL LWDS Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x53 | Can Signal Timeout des Subcontrollers SZL LWDS Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x54 | Can Signal SZL in diesem Zündungszyklus nie dagewesen LWDS Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x55 | SZL Winkel außerhalb erwartetem Band LWDS Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x56 | Differenz zwischen redundaten Lenkwinkelsignalen ist zu groß LWDS Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x57 | Differenz nach Timeout zwischen aufeinanderfolgenden Signalwerten zu groß LWSD Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x58 | Kein 2uC SZL LWDS Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x59 | SZL neu verbaut oder neu abgeglichen LWDS Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x5A | SZL Typ wurde nicht empfangen LWDS Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x5B | unbenutzt LWDS Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x5C | unbenutzt LWDS Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x5D | unbenutzt LWDS Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x5E | unbenutzt LWDS Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x5F | unbenutzt LWDS Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x60 | Fehler Integral 1 MDYN Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x61 | Fehler Integral 2 MDYN Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x62 | unbenutzt MDYN Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x63 | unbenutzt MDYN Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x64 | unbenutzt MDYN Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x65 | unbenutzt MDYN Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x66 | unbenutzt MDYN Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x67 | unbenutzt MDYN Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x68 | unbenutzt MDYN Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x69 | unbenutzt MDYN Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x6A | unbenutzt MDYN Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x6B | unbenutzt MDYN Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x6C | unbenutzt MDYN Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x6D | unbenutzt MDYN Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x6E | unbenutzt MDYN Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x6F | unbenutzt MDYN Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0x70 | GMK keine Lenkanforderung Bit 0 | 0/1 | -- | 0x0001 | -- | - | - | - |
| 0x71 | GMK Lenkanforderung Bit 1 | 0/1 | -- | 0x0002 | -- | - | - | - |
| 0x72 | GMK irreversibel deaktiviert Bit 2 | 0/1 | -- | 0x0004 | -- | - | - | - |
| 0x73 | GMK Timeout Bit 3 | 0/1 | -- | 0x0008 | -- | - | - | - |
| 0x74 | GMK Fehlerwert Bit 4 | 0/1 | -- | 0x0010 | -- | - | - | - |
| 0x75 | GMK CRC/Alive Fehler Bit 5 | 0/1 | -- | 0x0020 | -- | - | - | - |
| 0x76 | GMK Teilsollwert zu hoch Bit 6 | 0/1 | -- | 0x0040 | -- | - | - | - |
| 0x77 | GMK Regelung zu lang Bit 7 | 0/1 | -- | 0x0080 | -- | - | - | - |
| 0x78 | GMK Teilsollwert ins Modell ungleich NULL Bit 8 | 0/1 | -- | 0x0100 | -- | - | - | - |
| 0x79 | DSC Status passiv Bit 9 | 0/1 | -- | 0x0200 | -- | - | - | - |
| 0x7A | DSC Status defekt Bit 10 | 0/1 | -- | 0x0400 | -- | - | - | - |
| 0x7B | DSC Status DTC Bit 11 | 0/1 | -- | 0x0800 | -- | - | - | - |
| 0x7C | unbenutzt GMK Bit 12 | 0/1 | -- | 0x1000 | -- | - | - | - |
| 0x7D | ECO Status Bit 13 | 0/1 | -- | 0x2000 | -- | - | - | - |
| 0x7E | Motordynamik SW1 Bit 14 | 0/1 | -- | 0x4000 | -- | - | - | - |
| 0x7F | Signalfehler AY,RR Bit 15 | 0/1 | -- | 0x8000 | -- | - | - | - |
| 0xFF | ohne Bedeutung | 1 | -- | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-harttexteerweitert"></a>
### HARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxx00 | 100 | Allgemeiner Fehler |
| xxxxxx01 | 101 | FSP uebergelaufen |
| xxxxxx10 | 110 | FSP nicht uebergelaufen |
| xxxxxx11 | 111 | Status ungueltig |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 108 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x6001 | KFC_NEC_ERR_1 |
| 0x6002 | KFC_NEC_ERR_2 |
| 0x6003 | KFC_NEC_ERR_3 |
| 0x6004 | KFC_NEC_ERR_4 |
| 0x6005 | KFC_NEC_ERR_5 |
| 0x6006 | KFC_NEC_ERR_6 |
| 0x6007 | KFC_NEC_ERR_7 |
| 0x6008 | KFC_NEC_ERR_8 |
| 0x6009 | KFC_PROG |
| 0x600A | KFC_COMM |
| 0x600B | KFC_EEPROMNR |
| 0x600C | KFC_EEPROMHR |
| 0x600D | KFC_KLD |
| 0x600E | KFC_ROM |
| 0x600F | KFC_TBD15 |
| 0x6010 | KFC_CORE |
| 0x6011 | KFC_TBD17 |
| 0x6012 | KFC_OS |
| 0x6013 | KFC_MLW_INVALID |
| 0x6014 | KFC_VX_REF |
| 0x6015 | KFC_DPSI1 |
| 0x6016 | KFC_TBD22 |
| 0x6017 | KFC_DPSI2 |
| 0x6018 | KFC_TBD24 |
| 0x6019 | KFC_AY1 |
| 0x601A | KFC_TBD26 |
| 0x601B | KFC_AY2 |
| 0x601C | KFC_TBD28 |
| 0x601D | KFC_DEH |
| 0x601E | KFC_TBD30 |
| 0x601F | KFC_TBD31 |
| 0x6020 | KFC_LWS |
| 0x6021 | KFC_MPC_POSCTRL_ERR |
| 0x6022 | KFC_VINCOMP |
| 0x6023 | KFC_CONFIG |
| 0x6024 | KFC_MPC_BOOT_FLASH |
| 0x6025 | KFC_NEC_UPDATE |
| 0x6026 | KFC_MPC_SCI_ERR |
| 0x6027 | KFC_INV_SER_SLZ |
| 0x6028 | KFC_GEST_1 |
| 0x6029 | KFC_GEST_2 |
| 0x602A | KFC_GEST_3 |
| 0x602B | KFC_LOW_VOLTAGE |
| 0x602C | KFC_LWS_FS |
| 0x602D | KFC_LWS_FS_OFF |
| 0x602E | KFC_SENSOR_DRIVE |
| 0x602F | KFC_CANA |
| 0x6030 | KFC_CANB |
| 0x6031 | KFC_CANA_Y1 |
| 0x6032 | KFC_CANA_Y2 |
| 0x6033 | KFC_CANA_DSC_VWHL |
| 0x6034 | KFC_CANA_LWSRAD |
| 0x6035 | KFC_CANA_DSC_REGULATION |
| 0x6036 | KFC_CANA_SZL_LWDS |
| 0x6037 | KFC_TBD55 |
| 0x6038 | KFC_TBD56 |
| 0x6039 | KFC_CANB_DSC_STAT |
| 0x603A | KFC_CANB_DME_TORQ1 |
| 0x603B | KFC_CANB_DME_TORQ3 |
| 0x603C | KFC_CANB_DME_MOTORDAT |
| 0x603D | KFC_GMK |
| 0x603E | KFC_CANB_CAS_KLEMMEN |
| 0x603F | KFC_TBD63 |
| 0x6040 | KFC_CANB_KI_KM |
| 0x6041 | KFC_TBD65 |
| 0x6042 | KFC_CANA_SZL_LWDS_INIT |
| 0x6043 | KFC_RSCAN |
| 0x6044 | KFC_TBD68 |
| 0x6101 | NKFC_CAN |
| 0x6102 | NKFC_CCU |
| 0x6103 | NKFC_EEPROMNR |
| 0x6104 | NKFC_US |
| 0x6105 | NKFC_EPROM |
| 0x6106 | NKFC_IWD |
| 0x6107 | NKFC_COMP |
| 0x6108 | NKFC_RAM |
| 0x6109 | NKFC_RELAIS |
| 0x610A | NKFC_SMCURR |
| 0x610B | NKFC_SMPOS |
| 0x610C | NKFC_SMVOLT |
| 0x610D | NKFC_PROG |
| 0x610E | NKFC_EEPROMHR |
| 0x610F | NKFC_MOD_MC |
| 0x6110 | NKFC_BRAKE |
| 0x6111 | NKFC_COMM |
| 0x6112 | NKFC_MTEMP |
| 0x6113 | NKFC_LWSSUPP |
| 0x6114 | NKFC_DPOP |
| 0x6115 | NKFC_MPC |
| 0x6116 | NKFC_MPC_SUBS_1 |
| 0x6117 | NKFC_MPC_SUBS_2 |
| 0x6118 | NKFC_MPC_SUBS_3 |
| 0x6119 | NKFC_MPC_SUBS_4 |
| 0x611A | NKFC_MPC_SUBS_5 |
| 0x611B | NKFC_MPC_SUBS_6 |
| 0x611C | NKFC_MPC_SUBS_7 |
| 0x611D | NKFC_MPC_SUBS_8 |
| 0x611E | NKFC_MPC_SUBS_9 |
| 0x611F | NKFC_MTEMP_SENS |
| 0x6120 | NKFC_EN_CHOKE |
| 0x6121 | NKFC_ST |
| 0x6122 | NKFC_ECO |
| 0x6123 | NKFC_COMP_CAN |
| 0x6124 | NKFC_DEBUG_ACTIVE |
| 0x6125 | NKFC_SELFLOCK |
| 0x6126 | NKFC_CANA_WHEELSPEED |
| 0x6127 | NKFC_LOWVOLT |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00002211 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | INFO_A | INFO_B | INFO_C | INFO_D |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 19 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Reihenfolge der Ablage | - | -- | unsigned char | - | - | - | - |
| 0x02 | Position im FSP | - | -- | unsigned char | - | - | - | - |
| 0x10 | ZF-LS FehlerCode | - | high | unsigned int | -- | - | - | - |
| 0x11 | ZF-LS FehlerArt | - | high | unsigned int | -- | - | - | - |
| 0x12 | ZF-LS Statuswort | Hex | high | unsigned int | -- | - | - | - |
| 0x20 | Fahrzeuggeschwindigkeit | km/h | -- | signed char | -- | 2 | 1 | 0 |
| 0x21 | Querbeschleunigung | m/(s*s) | -- | signed char | -- | 1 | 7 | 0 |
| 0x22 | Gierrate | rad/s | -- | signed char | -- | 1 | 70 | 0 |
| 0x23 | Summenlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x24 | Fahrerlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x25 | Versorgungsspannung | Volt | -- | unsigned char | -- | 1 | 12.75 | 0 |
| 0x26 | ohne Bedeutung | - | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x27 | Weckleitung | - | -- | unsigned char | - | - | - | - |
| 0x28 | Klemme15 | - | -- | unsigned char | - | - | - | - |
| 0x29 | SG-Stati | - | -- | unsigned char | - | - | - | - |
| 0x2A | Sperrenstatus | - | -- | unsigned char | - | - | - | - |
| 0x30 | Ersatzmassnahmen | Hex | high | signed long | -- | - | - | - |
| 0x40 | DTC spezifisch | Hex | high | unsigned int | -- | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 8 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxx00 | 100 | Allgemeiner Fehler |
| xxxxxx01 | 101 | NEC Fehlerspeicher uebergelaufen |
| xxxxxx10 | 110 | MPC Fehlerspeicher uebergelaufen |
| xxxxxx11 | 111 | Ueberlauf ungueltig |
| xxxx00xx | 200 | Allgemeiner Fehler |
| xxxx01xx | 201 | AFS ausgefallen |
| xxxx10xx | 210 | AFS gestoert |
| xxxx11xx | 211 | Status ungueltig |

<a id="table-lowlevel"></a>
### LOWLEVEL

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x02 |

<a id="table-systemstate"></a>
### SYSTEMSTATE

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B |

<a id="table-errorstate"></a>
### ERRORSTATE

Dimensions: 1 rows × 33 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR | UW17_NR | UW18_NR | UW19_NR | UW20_NR | UW21_NR | UW22_NR | UW23_NR | UW24_NR | UW25_NR | UW26_NR | UW27_NR | UW28_NR | UW29_NR | UW30_NR | UW31_NR | UW32_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 32 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 | 0x16 | 0x17 | 0x18 | 0x19 | 0x1A | 0x1B | 0x1C | 0x1D | 0x1E | 0x1F | 0x20 | 0x21 | 0x22 | 0x23 | 0x24 | 0x25 | 0x26 | 0x27 | 0x28 | 0x29 | 0x2A | 0x2B | 0x2C | 0x2D | 0x2E | 0x2F |

<a id="table-dpsi"></a>
### DPSI

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x30 | 0x31 | 0x32 | 0x33 | 0x34 | 0x35 | 0x36 | 0x37 | 0x38 | 0x39 | 0x3A | 0x3B | 0x3C | 0x3D | 0x3E | 0x3F |

<a id="table-deh"></a>
### DEH

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x40 | 0x41 | 0x42 | 0x43 | 0x44 | 0x45 | 0x46 | 0x47 | 0x48 | 0x49 | 0x4A | 0x4B | 0x4C | 0x4D | 0x4E | 0x4F |

<a id="table-lws"></a>
### LWS

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x50 | 0x51 | 0x52 | 0x53 | 0x54 | 0x55 | 0x56 | 0x57 | 0x58 | 0x59 | 0x5A | 0x5B | 0x5C | 0x5D | 0x5E | 0x5F |

<a id="table-mdyn"></a>
### MDYN

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x60 | 0x61 | 0x62 | 0x63 | 0x64 | 0x65 | 0x66 | 0x67 | 0x68 | 0x69 | 0x6A | 0x6B | 0x6C | 0x6D | 0x6E | 0x6D |

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
| 0x01 | i.O. |
| 0x02 | n.i.O. |
| 0xFF | unbekannter DPRAM Status |

<a id="table-einaus"></a>
### EINAUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Ein |
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

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nachricht i.O. |
| 0x02 | Nachricht init |
| 0x04 | Nachricht timeout |
| 0x08 | Nachricht Inhalt ungueltig |
| 0x10 | Nachrichten Ueberpruefung fehlerhaft |
| 0x20 | Nachricht Sampling |
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
| 0x00 | i.O., volle Dynamik |
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
| 0x00 | FLASH_BOOT |
| 0x01 | FLASH_DRIVE |
| 0x02 | FLASH_BBIND |
| 0x03 | FLASH_NOT |
| 0x04 | FLASH_UNDEF |
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
| 0x000A | KFC_COMM | Communication error |
| 0x000B | KFC_EEPROMNR | EEPROM No Risk |
| 0x000C | KFC_EEPROMHR | EEPROM High Risk |
| 0x000D | KFC_KLD | KLD Position/Speed |
| 0x000E | KFC_ROM | ROM-Test |
| 0x000F | KFC_TBD15 | TBD15 |
| 0x0010 | KFC_CORE | Core-Test |
| 0x0011 | KFC_TBD17 | TBD17 |
| 0x0012 | KFC_OS | ERCOSEK Fehler |
| 0x0013 | KFC_MLW_INVALID | Motorlagewinkel ungueltig |
| 0x0014 | KFC_VX_REF | Geschwindigkeit unklar |
| 0x0015 | KFC_DPSI1 | Gierratensensor 1 |
| 0x0016 | KFC_TBD22 | TBD22 |
| 0x0017 | KFC_DPSI2 | Gierratensensor 2 |
| 0x0018 | KFC_TBD24 | TBD24 |
| 0x0019 | KFC_AY1 | Querbeschleunigungssensor 1 |
| 0x001A | KFC_TBD26 | TBD26 |
| 0x001B | KFC_AY2 | Querbeschleunigungssensor 2 |
| 0x001C | KFC_TBD28 | TBD28 |
| 0x001D | KFC_DEH | Lenkwinkelueberwachung |
| 0x001E | KFC_TBD30 | TBD30 |
| 0x001F | KFC_TBD31 | TBD31 |
| 0x0020 | KFC_LWS | Redundanzueberwachung Lenkradwinkel oben |
| 0x0021 | KFC_MPC_POSCTRL_ERR | Motordynamikueberwachung |
| 0x0022 | KFC_VINCOMP | Fahrgestellnummernvergleich |
| 0x0023 | KFC_CONFIG | Codierdatenfehler |
| 0x0024 | KFC_MPC_BOOT_FLASH | SG haengt im Bootblock oder Flashdatenfehler |
| 0x0025 | KFC_NEC_UPDATE | NEC Prozessor macht gerade einen Update oder haengt im Update |
| 0x0026 | KFC_MPC_SCI_ERR | kein 2 Prozessor SZL |
| 0x0027 | KFC_INV_SER_SLZ | ungueltige Seriennummer vom SZL |
| 0x0028 | KFC_GEST_1 | AFS gestoert 1 |
| 0x0029 | KFC_GEST_2 | AFS gestoert 2 |
| 0x002A | KFC_GEST_3 | AFS gestoert 3 |
| 0x002B | KFC_LOW_VOLTAGE | Unterspannung, kein Abschalten |
| 0x002C | KFC_LWS_FS | Fehler Summenlenkwinkelbeziehung |
| 0x002D | KFC_LWS_FS_OFF | keine Ueberwachung der Winkelsummenbeziehung |
| 0x002E | KFC_SENSOR_DRIVE | positive Identifikation des Fahrdynamiksensors |
| 0x002F | KFC_CANA | Error of CANA controller (F-CAN) |
| 0x0030 | KFC_CANB | Error of CANB controller (PT-CAN) |
| 0x0031 | KFC_CANA_Y1 | Error ID Gierrate Antwort 1 |
| 0x0032 | KFC_CANA_Y2 | Error ID Gierrate Antwort 2 |
| 0x0033 | KFC_CANA_DSC_VWHL | Error ID Radgeschwindigkeit |
| 0x0034 | KFC_CANA_LWSRAD | Error ID Summenlenkwinkel |
| 0x0035 | KFC_CANA_DSC_REGULATION | Error ID Regeleingriffe DSC AFS |
| 0x0036 | KFC_CANB_SZL_LWDS | Error ID Lenkradwinkel oben |
| 0x0037 | KFC_TBD55 | TBD55 |
| 0x0038 | KFC_TBD56 | TBD56 |
| 0x0039 | KFC_CANB_DSC_STAT | Error ID Status DSC |
| 0x003A | KFC_CANB_DME_TORQ1 | Error ID DME Bremslichtschalter |
| 0x003B | KFC_CANB_DME_TORQ3 | Error ID DME Motormoment |
| 0x003C | KFC_CANB_DME_MOTORDAT | Error ID DME Motordaten |
| 0x003D | KFC_GMK | GMK Fehler |
| 0x003E | KFC_CANB_CAS_KLEMMEN | Error ID CAS Klemmenstatus |
| 0x003F | KFC_TBD63 | TBD63 |
| 0x0040 | KFC_CANB_KI_KM | Error ID Kombianzeige Kilometerstand |
| 0x0041 | KFC_TBD65 | TBD65 |
| 0x0042 | KFC_CANA_SZL_LWDS_INIT | Error ID SZL Init Phase |
| 0x0043 | KFC_RSCAN | DPRAM Fehler in der Aufstartphase |
| 0x0044 | KFC_TBD68 | TBD68 |
| 0xFFFF | ------------ | unbekannte MPC Fehlernummer |

<a id="table-necfehlercode"></a>
### NECFEHLERCODE

Dimensions: 41 rows × 3 columns

| WERT | CODE | TEXT |
| --- | --- | --- |
| 0x0000 | NKFC_OK | kein Fehler eingetragen |
| 0x0001 | NKFC_CAN | CAN |
| 0x0002 | NKFC_CCU | outputstage temperature |
| 0x0003 | NKFC_EEPROMNR | EEPROM: no security risk |
| 0x0004 | NKFC_US | sensor supply voltage |
| 0x0005 | NKFC_EPROM | ROM checksum |
| 0x0006 | NKFC_IWD | intelligent watchdog |
| 0x0007 | NKFC_COMP | diversitaeres Rechnen |
| 0x0008 | NKFC_RAM | RAM |
| 0x0009 | NKFC_RELAIS | relais |
| 0x000A | NKFC_SMCURR | servomotor current |
| 0x000B | NKFC_SMPOS | servomotor positionsensor |
| 0x000C | NKFC_SMVOLT | servomotor phase voltage |
| 0x000D | NKFC_PROG | program error |
| 0x000E | NKFC_EEPROMHR | EEPROM: high security risk |
| 0x000F | NKFC_MOD_MC | module MC, program error |
| 0x0010 | NKFC_BRAKE | locking pin |
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
| 0x001E | NKFC_MPC_SUBS_9 | Error from MPC |
| 0x001F | NKFC_MTEMP_SENS | motortemp. sensor failed |
| 0x0020 | NKFC_EN_CHOKE | supply for driver to low |
| 0x0021 | NKFC_ST | SERVO Ventil Error |
| 0x0022 | NKFC_ECO | ECO Ventil Error |
| 0x0023 | NKFC_COMP_CAN | AFS Teilsollwerte F-CAN |
| 0x0024 | NKFC_DEBUG_ACTIVE | NEC Debug Botschaften aktiv |
| 0x0025 | NKFC_SELFLOCK | Selbsthemmungsueberwachung |
| 0x0026 | NKFC_CANA_WHEELSPEED | Botschaft Radgeschwindigkeiten |
| 0x0027 | NKFC_LOWVOLT | Versorgungsspannung Kl. 30 (&lt; 7.5 Volt) |
| 0xFFFF | ------------ | unbekannte NEC Fehlernummer |

<a id="table-necfehlertyp"></a>
### NECFEHLERTYP

Dimensions: 91 rows × 3 columns

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
| 0x0020 | KFA_RA_MC | range error in module MC Volt |
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
| 0x0031 | KFA_DISCHARGE | tbd |
| 0x0032 | KFA_LKMPC | MPC can t switch off; relais SC plus |
| 0x0033 | KFA_LKNEC | NEC can t switch off |
| 0x0034 | KFA_LKWD | Module MC, program error |
| 0x0035 | KFA_I3_NOT_VALID | CG 120 can t switch off |
| 0x0036 | KFA_OCTMP | open circuit temp. sensor |
| 0x0037 | KFA_SCTMP | short circuit temp. sensor |
| 0x0038 | KFA_DXSERVER | DX Dualport RAM |
| 0x0039 | KFA_STACK | mpu Stack |
| 0x003A | KFA_GEN_1 | frozen AD converter |
| 0x003B | KFA_GEN_2 | tbd |
| 0x003C | KFA_GEN_3 | MPC can t switch off; relais SC plus |
| 0x003D | KFA_GEN_4 | NEC can t switch off |
| 0x003E | KFA_GEN_5 | Module MC, program error |
| 0x003F | KFA_GEN_6 | CG 120 can t switch off |
| 0x0040 | KFA_GEN_7 | tbd |
| 0x0041 | KFA_GEN_8 | tbd |
| 0x0042 | KFA_GEN_9 | tbd |
| 0x0043 | KFA_GEN_10 | tbd |
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
| 0x0053 | KFA_VERIFY | tbd |
| 0x0054 | KFA_DRV_LV | Driver Low Voltage |
| 0x0055 | KFA_DRV_SC | Driver Shortcut |
| 0x0056 | KFA_DRV_OT | Driver over temp |
| 0x0057 | KFA_SHORTCUT_LOAD_IN | Masseschluss Zuleitung SERVO oder ECO |
| 0x0058 | KFA_LOAD_BRACKE_OR_SHORTCUT_OUT | Lastabriss oder Masseschluss Rueckleitung oder Uebertemperatur |
| 0x0059 | KFA_CAN_HW | CAN Hardwaredefekt |
| 0xFFFF | ---------------- | unbekannter NEC Fehlertyp bzw Art |

<a id="table-ausein"></a>
### AUSEIN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ein |
| 0x01 | Aus |
| 0xFF | unbekannter Status |

<a id="table-sperre"></a>
### SPERRE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sperre geschlossen |
| 0x01 | Sperre oeffnen: starten |
| 0x02 | Sperre oeffnet |
| 0x03 | Sperre geoeffnet |
| 0x04 | Wartezeit Motorauslauf: starten |
| 0x05 | Warten bis Motor steht |
| 0xFF | unbekannter Sperrenstatus |

<a id="table-mpcrev"></a>
### MPCREV

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x3620 | rev B 0L08N |
| 0xFFFF | unbekannte MPC Maske |

<a id="table-bitgmkafs"></a>
### BITGMKAFS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine GMK-Lenkanforderung aber GMK-Funktion |
| 0x01 | GMK-Lenkanforderung |
| 0x02 | GMK-reversibel deaktiviert |
| 0x03 | GMK-irreversibel deaktiviert |
| 0xFF | unbekannter Status |

<a id="table-gmkqualbit0"></a>
### GMKQUALBIT0

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | GMK-Anforderung DSC |
| 0x01 | keine GMK-Anforderung DSC |
| 0xFF | unbekannter Status |

<a id="table-gmkqualbit1"></a>
### GMKQUALBIT1

Dimensions: 3 rows × 2 columns

| BIT1_NR | BIT1_TEXT |
| --- | --- |
| 0x00 | nicht-zuruecknehmen der Gierratenregelung |
| 0x01 | zuruecknehmen der Gierratenregelung |
| 0xFF | unbekannter Status |

<a id="table-gmkqualbit2"></a>
### GMKQUALBIT2

Dimensions: 3 rows × 2 columns

| BIT2_NR | BIT2_TEXT |
| --- | --- |
| 0x00 | kein temporaerer Fehler DSC |
| 0x01 | temporaerer Fehler DSC |
| 0xFF | unbekannter Status |

<a id="table-gmkqualbit3"></a>
### GMKQUALBIT3

Dimensions: 3 rows × 2 columns

| BIT3_NR | BIT3_TEXT |
| --- | --- |
| 0x00 | kein Fehler DSC |
| 0x01 | Fehler DSC |
| 0xFF | unbekannter Status |

<a id="table-gmkqualbit4"></a>
### GMKQUALBIT4

Dimensions: 3 rows × 2 columns

| BIT4_NR | BIT4_TEXT |
| --- | --- |
| 0x00 | kein temporaerer Fehler AFS |
| 0x01 | temporaerer Fehler AFS |
| 0xFF | unbekannter Status |

<a id="table-gmkqualbit5"></a>
### GMKQUALBIT5

Dimensions: 3 rows × 2 columns

| BIT5_NR | BIT5_TEXT |
| --- | --- |
| 0x00 | kein Fehler AFS |
| 0x01 | Fehler AFS |
| 0xFF | unbekannter Status |

<a id="table-lwgquadrant"></a>
### LWGQUADRANT

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | Quadrant gueltig |
| 0x01 | Quadrant nicht gueltig |
| 0xFF | unbekannter Status |

<a id="table-szlprozinfo"></a>
### SZLPROZINFO

Dimensions: 3 rows × 2 columns

| SZL_PROZ_NR | SZL_PROZ_TEXT |
| --- | --- |
| 0x00 | SZL Ein-Prozessor ; kein AFS |
| 0xA0 | SZL Zwei-Prozessor ; AFS |
| 0xFF | unbekannter Status |

<a id="table-gmk"></a>
### GMK

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x70 | 0x71 | 0x72 | 0x73 | 0x74 | 0x75 | 0x76 | 0x77 | 0x78 | 0x79 | 0x7A | 0x7B | 0x7C | 0x7D | 0x7E | 0x7F |

<a id="table-gmkqualbit6"></a>
### GMKQUALBIT6

Dimensions: 3 rows × 2 columns

| BIT6_NR | BIT6_TEXT |
| --- | --- |
| 0x00 | keine Ueberschreitung Betrag |
| 0x01 | Ueberschreitung Betrag |
| 0xFF | unbekannter Status |

<a id="table-gmkqualbit7"></a>
### GMKQUALBIT7

Dimensions: 3 rows × 2 columns

| BIT7_NR | BIT7_TEXT |
| --- | --- |
| 0x00 | keine Ueberschreitung Zeit |
| 0x01 | Ueberschreitung Zeit |
| 0xFF | unbekannter Status |

<a id="table-info-a"></a>
### INFO_A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x01 | 0x02 | 0x10 | 0x11 | 0x12 |

<a id="table-info-b"></a>
### INFO_B

Dimensions: 1 rows × 12 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11 | 0x20 | 0x21 | 0x22 | 0x23 | 0x24 | 0x25 | 0x26 | 0x27 | 0x28 | 0x29 | 0x2A |

<a id="table-info-c"></a>
### INFO_C

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x30 |

<a id="table-info-d"></a>
### INFO_D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x40 |

<a id="table-mdyqualbit0"></a>
### MDYQUALBIT0

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | untere Schwelle 1 |
| 0xFF | unbekannter Status |

<a id="table-mdyqualbit1"></a>
### MDYQUALBIT1

Dimensions: 3 rows × 2 columns

| BIT1_NR | BIT1_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | obere Schwelle 2 |
| 0xFF | unbekannter Status |

<a id="table-lwdsqualbit0"></a>
### LWDSQUALBIT0

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | Nutzsignale vorhanden |
| 0x01 | keine Nutzsignale vorhanden |
| 0xFF | unbekannter Status |

<a id="table-lwdsqualbit1"></a>
### LWDSQUALBIT1

Dimensions: 3 rows × 2 columns

| BIT1_NR | BIT1_TEXT |
| --- | --- |
| 0x00 | kein Fehlerverdacht |
| 0x01 | Fehlerverdacht |
| 0xFF | unbekannter Status |

<a id="table-lwdsqualbit2"></a>
### LWDSQUALBIT2

Dimensions: 3 rows × 2 columns

| BIT2_NR | BIT2_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Fehler (im aktiven Zuendungszyklus irreversiber Fehler) |
| 0xFF | unbekannter Status |

<a id="table-lwdsqualbit3"></a>
### LWDSQUALBIT3

Dimensions: 3 rows × 2 columns

| BIT3_NR | BIT3_TEXT |
| --- | --- |
| 0x00 | Ersatzsignal nicht vorhanden |
| 0x01 | Ersatzsignal wird gesendet (irreversiber Zustand im aktuellen Zuendungszyklus) |
| 0xFF | unbekannter Status |

<a id="table-lwdsqualbit4"></a>
### LWDSQUALBIT4

Dimensions: 3 rows × 2 columns

| BIT4_NR | BIT4_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Fehler im Status Summenlenkwinkel oder Motorlagewinkel gesetzt |
| 0xFF | unbekannter Status |

<a id="table-lwgqualbit0"></a>
### LWGQUALBIT0

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | Nutzsignale vorhanden |
| 0x01 | keine Nutzsignale vorhanden |
| 0xFF | unbekannter Status |

<a id="table-lwgqualbit1"></a>
### LWGQUALBIT1

Dimensions: 3 rows × 2 columns

| BIT1_NR | BIT1_TEXT |
| --- | --- |
| 0x00 | kein Fehlerverdacht |
| 0x01 | Fehlerverdacht |
| 0xFF | unbekannter Status |

<a id="table-lwgqualbit2"></a>
### LWGQUALBIT2

Dimensions: 3 rows × 2 columns

| BIT2_NR | BIT2_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Fehler (im aktiven Zuendungszyklus irreversibler Fehler) |
| 0xFF | unbekannter Status |

<a id="table-lwgqualbit3"></a>
### LWGQUALBIT3

Dimensions: 3 rows × 2 columns

| BIT3_NR | BIT3_TEXT |
| --- | --- |
| 0x00 | Ersatzsignal nicht vorhanden |
| 0x01 | Ersatzsignal vorhanden |
| 0xFF | unbekannter Status |

<a id="table-lwgqualbit4"></a>
### LWGQUALBIT4

Dimensions: 3 rows × 2 columns

| BIT4_NR | BIT4_TEXT |
| --- | --- |
| 0x00 | kein Fehler Ersatzsignal |
| 0x01 | Fehler Ersatzsignal (Fahrerlenk/Motorlage-winkel) |
| 0xFF | unbekannter Status |

<a id="table-lwgqualbit5"></a>
### LWGQUALBIT5

Dimensions: 3 rows × 2 columns

| BIT5_NR | BIT5_TEXT |
| --- | --- |
| 0x00 | Sektor (Quadrant) bestimmt |
| 0x01 | Sektor (Quadrant) nicht bestimmt |
| 0xFF | unbekannter Status |

<a id="table-lwgqualbit6"></a>
### LWGQUALBIT6

Dimensions: 3 rows × 2 columns

| BIT6_NR | BIT6_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Fehler WSG |
| 0xFF | unbekannter Status |

<a id="table-refvxqualbit0"></a>
### REFVXQUALBIT0

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | Nutzsignal vorhanden |
| 0x01 | kein Nutzsignal vorhanden |
| 0xFF | unbekannter Status |

<a id="table-refvxqualbit1"></a>
### REFVXQUALBIT1

Dimensions: 3 rows × 2 columns

| BIT1_NR | BIT1_TEXT |
| --- | --- |
| 0x00 | Nutzsignal sicher |
| 0x01 | Nutzsignal unsicher |
| 0xFF | unbekannter Status |

<a id="table-refvxqualbit2"></a>
### REFVXQUALBIT2

Dimensions: 3 rows × 2 columns

| BIT2_NR | BIT2_TEXT |
| --- | --- |
| 0x00 | Fahrtrichtung sicher |
| 0x01 | Nutzsignal unsicher |
| 0xFF | unbekannter Status |

<a id="table-refvxqualbit3"></a>
### REFVXQUALBIT3

Dimensions: 3 rows × 2 columns

| BIT3_NR | BIT3_TEXT |
| --- | --- |
| 0x00 | kein DF-Fehler |
| 0x01 | mindestens 1 DF-Fehler |
| 0xFF | unbekannter Status |

<a id="table-ayqualbit0"></a>
### AYQUALBIT0

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | Nutzsignal vorhanden |
| 0x01 | kein Nutzsignal vorhanden |
| 0xFF | unbekannter Status |

<a id="table-ayqualbit1"></a>
### AYQUALBIT1

Dimensions: 3 rows × 2 columns

| BIT1_NR | BIT1_TEXT |
| --- | --- |
| 0x00 | Nutzsignal ueberwachbar |
| 0x01 | Nutzsignal nicht ueberwachbar, oder kein Abgleichwert von beiden Signalen |
| 0xFF | unbekannter Status |

<a id="table-ayqualbit2"></a>
### AYQUALBIT2

Dimensions: 3 rows × 2 columns

| BIT2_NR | BIT2_TEXT |
| --- | --- |
| 0x00 | Offsetabgleich vorhanden |
| 0x01 | kein Offsetabgleich vorhanden (auch kein EEPROM) |
| 0xFF | unbekannter Status |

<a id="table-ayqualbit4"></a>
### AYQUALBIT4

Dimensions: 3 rows × 2 columns

| BIT4_NR | BIT4_TEXT |
| --- | --- |
| 0x00 | kein Fehlerverdacht |
| 0x01 | Fehlerverdacht oder temporaerer Fehler |
| 0xFF | unbekannter Status |

<a id="table-ayqualbit5"></a>
### AYQUALBIT5

Dimensions: 3 rows × 2 columns

| BIT5_NR | BIT5_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Fehler (im aktuellen Zuendungszyklus irreversibler Fehler) |
| 0xFF | unbekannter Status |

<a id="table-rrqualbit0"></a>
### RRQUALBIT0

Dimensions: 3 rows × 2 columns

| BIT0_NR | BIT0_TEXT |
| --- | --- |
| 0x00 | Nutzsignal vorhanden |
| 0x01 | kein Nutzsignal vorhanden |
| 0xFF | unbekannter Status |

<a id="table-rrqualbit1"></a>
### RRQUALBIT1

Dimensions: 3 rows × 2 columns

| BIT1_NR | BIT1_TEXT |
| --- | --- |
| 0x00 | Nutzsignal ueberwachbar |
| 0x01 | Nutzsignal nicht ueberwachbar, oder kein Abgleichwert von beiden Signalen |
| 0xFF | unbekannter Status |

<a id="table-rrqualbit2"></a>
### RRQUALBIT2

Dimensions: 3 rows × 2 columns

| BIT2_NR | BIT2_TEXT |
| --- | --- |
| 0x00 | Offsetabgleich vorhanden |
| 0x01 | kein Offsetabgleich vorhanden (auch kein EEPROM) |
| 0xFF | unbekannter Status |

<a id="table-rrqualbit3"></a>
### RRQUALBIT3

Dimensions: 3 rows × 2 columns

| BIT3_NR | BIT3_TEXT |
| --- | --- |
| 0x00 | Empfindlichkeitsabgleich vorhanden |
| 0x01 | Empfindlichkeitfehler oder kein Empfindlichkeitsabgleich vorhanden (auch kein EEPROM) |
| 0xFF | unbekannter Status |

<a id="table-rrqualbit4"></a>
### RRQUALBIT4

Dimensions: 3 rows × 2 columns

| BIT4_NR | BIT4_TEXT |
| --- | --- |
| 0x00 | kein Fehlerverdacht |
| 0x01 | Fehlerverdacht oder temporaerer Fehler |
| 0xFF | unbekannter Status |

<a id="table-rrqualbit5"></a>
### RRQUALBIT5

Dimensions: 3 rows × 2 columns

| BIT5_NR | BIT5_TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Fehler (im aktuellen Zuendungszyklus irreversibler Fehler) |
| 0xFF | unbekannter Status |

<a id="table-bmwmode"></a>
### BMWMODE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | DES_MASTER_INITIALISATION |
| 0x02 | DES_MASTER_PRE_DRIVE |
| 0x04 | DES_MASTER_NORMAL_MODE |
| 0x08 | DES_MASTER_POST_RUN |
| 0x10 | DES_MASTER_POWER_OFF |
| 0x20 | DES_MASTER_ERROR_MODE |
| 0xFF | unbekannter Status |

<a id="table-fertig"></a>
### FERTIG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht fertig |
| 0x01 | fertig |
| 0xFF | unbekannter Status |

<a id="table-dxjob"></a>
### DXJOB

Dimensions: 23 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | DX_NOTHING |
| 0x02 | DX_WR_EEPROM |
| 0x03 | DX_RD_EEPROM |
| 0x04 | DX_WR_RAM |
| 0x05 | DX_RD_RAM_ROM |
| 0x06 | DX_STATUS |
| 0x07 | DX_STOP |
| 0x08 | DX_OK |
| 0x09 | DX_FSP_CLEAR_NEC |
| 0x0A | DX_FSP_SAVE_MPC |
| 0x0B | DX_FSP_RESTORE_MPC |
| 0x0C | DX_RD_NEC_FSP |
| 0x0D | DX_SWITCH_TO_BOOT |
| 0x0E | DX_CLR_FLASH_NEC |
| 0x0F | DX_FL_PROG |
| 0x10 | DX_VERI_NEC |
| 0x11 | DX_CHKSM |
| 0x12 | DX_RD_NEC_ID |
| 0x13 | DX_RESET_ALL |
| 0x14 | DX_AMBIENT_COND |
| 0x15 | DX_INIT_PARAMS |
| 0x16 | DX_INIT_RSCAN |
| 0xFF | unbekannter Status |

<a id="table-dxstatus"></a>
### DXSTATUS

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xFE01 | DX_IDLE |
| 0xFD02 | DX_STARTING |
| 0xFC03 | DX_STARTING_READY |
| 0xFB04 | DX_MPC_WR_CHKSM |
| 0xFA05 | DX_MPC_WR_DPR |
| 0xF906 | DX_MPC_WR_READY |
| 0xF807 | DX_NEC_RD_PARA |
| 0xF708 | DX_NEC_RD_CHKSM |
| 0xF609 | DX_NEC_RD_DPR |
| 0xF50A | DX_NEC_DO_JOB |
| 0xF40B | DX_NEC_WR_CHKSM |
| 0xF30C | DX_NEC_WR_DPR |
| 0xF20D | DX_NEC_WR_READY |
| 0xF10E | DX_MPC_RD_PARA |
| 0xF00F | DX_MPC_RD_CHKSM |
| 0xEF10 | DX_MPC_RD_DPR |
| 0xEE11 | DX_BREAK |
| 0xED12 | DX_FINISH |
| 0xEC13 | DX_FAILED |
| 0xFFFF | unbekannter Status |

<a id="table-statuslwgbit0"></a>
### STATUSLWGBIT0

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sensorwert NICHT gueltig (LWS fehlerhaft) |
| 0x01 | Sensorwert gueltig |
| 0xFF | unbekannter Status |

<a id="table-statuslwgbit1"></a>
### STATUSLWGBIT1

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sensor ist NICHT kalibriert |
| 0x01 | Sensor ist kalibriert |
| 0xFF | unbekannter Status |
