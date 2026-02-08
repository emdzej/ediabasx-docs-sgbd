# CAS.PRG

- Jobs: [166](#jobs)
- Tables: [23](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CAS  |
| ORIGIN | BMW EI-61 Martin Kaltenbrunner |
| REVISION | 7.000 |
| AUTHOR | SiemensVDO SV_C_BC_P3_PE_SW51 Lohberger, SiemensVDO SV_C_BC_P3_PE_SW51 Vaisman, SiemensVDO SV_C_BC_P3_PE_SW51 Palamari, SiemensVDO SV_C_BC_P3_PE_SW51 Tutsch |
| COMMENT | Keine Bemerkung  |
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
- [SG_VARIANTE_LESEN](#job-sg-variante-lesen) - Auslesen der SG-Variante auf Basis des Jobs Hardware Referenz lesen KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [STATUS_CAS_DIAGNOSE](#job-status-cas-diagnose) - All Inputs Read KWP2000: $30 InputOutputControlByLocalIdentifier LocalIdentifier=0x01 $01 ReportCurrentState Modus   : Default
- [STATUS_ISN](#job-status-isn) - 4 Byte des ISN KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $01 Modus   : Default
- [STATUS_MECHANISCHER_SCHLUESSELCODE](#job-status-mechanischer-schluesselcode) - 5 Byte des Mechanischer Schluesselcode KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $02 Modus   : Default
- [STATUS_SCHLUESSEL_FREQUENZ](#job-status-schluessel-frequenz) - Frequenz des Schluessels KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $03 Modus   : Default
- [STATUS_PROG_LOCATION_DATUM](#job-status-prog-location-datum) - Ort und Datum der ECU-Programmierung KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $04 Modus   : Default
- [STATUS_ZV_AUTHENTISIERUNG](#job-status-zv-authentisierung) - aktueller Status "ZV-Authentisierung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $05 Modus   : Default
- [STATUS_ELV_AUTHENTISIERUNG](#job-status-elv-authentisierung) - aktueller Status "ELV-Authentisierung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $05 Modus   : Default
- [STATUS_TRSP_INIT](#job-status-trsp-init) - aktueller Status "TRSP, Init-Kennung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $06 Modus   : Default
- [STATUS_TRSP_FAHRZYKLUSZAEHLER](#job-status-trsp-fahrzykluszaehler) - aktueller Status "TRSP, Fahrzykluszaehler" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $07 Modus   : Default
- [STATUS_CAS_INIT_KENNUNG](#job-status-cas-init-kennung) - aktueller Status "CAS, Init-Kennung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $08 Modus   : Default
- [STATUS_BDM_SPERREN](#job-status-bdm-sperren) - BDM-Sperren-Status Lesen KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $09 Modus   : Default
- [STATUS_EWS](#job-status-ews) - aktueller Status "EWS4 key" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Modus   : Default Zurücklesen verschiedener interner Stati für EWS4
- [STATUS_EWS4_SK](#job-status-ews4-sk) - aktueller Status "EWS4 secret keys" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Modus   : Default Lesen des SecretKey des Server (CAS) sowie Client (DME) für EWS4
- [STATUS_EWS4_KEY](#job-status-ews4-key) - aktueller Status "EWS4 key" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Modus   : Default
- [STATUS_DME_RINGBUFFER](#job-status-dme-ringbuffer) - aktueller Status "DME-RingBuffer" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0A Modus   : Default
- [STATUS_ZVFH_RINGBUFFER](#job-status-zvfh-ringbuffer) - aktueller Status "ZV/FH-Ringpuffer" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0B Modus   : Default
- [STATUS_FBD_TELEGRAMM](#job-status-fbd-telegramm) - letztes FBD-Telegramm KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0C Modus   : Default
- [STATUS_PA_TELEGRAMM](#job-status-pa-telegramm) - letztes PA-Telegramm KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0D Modus   : Default
- [STATUS_ICT_BYTE](#job-status-ict-byte) - Internal Circuit Test Byte (Siemens Data) KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0E Modus   : Default
- [STATUS_MLFB](#job-status-mlfb) - MLFB Data Siemens KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0F Modus   : Default
- [STATUS_SCHLUESSEL_DATEN](#job-status-schluessel-daten) - Auslesen der SCHLUESSELDATEN KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $10...$19 Modus   : Default
- [STATUS_SCHLUESSEL_BATTERIEZUSTAND](#job-status-schluessel-batteriezustand) - 1 Byte KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $22 Modus   : Default
- [STATUS_SYSTEM_FEHLER_KLSTRG](#job-status-system-fehler-klstrg) - 1 Byte KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $24 Modus   : Default
- [STATUS_BASESTATION](#job-status-basestation) - Auslesen der Basestation Status KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $25 Modus   : Default
- [STATUS_AKTUELL_SCHLUESSEL](#job-status-aktuell-schluessel) - aktuelle Schluessel KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $27 Modus   : Default
- [STATUS_TRANSPONDER_PAGE](#job-status-transponder-page) - Transponder Page KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2A Modus   : Default
- [STATUS_SET_PAGE_TRSP](#job-status-set-page-trsp) - Page TRSP KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2D Modus   : Default
- [STATUS_XTRSP_TEST_DATA](#job-status-xtrsp-test-data) - Test Data KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2F Modus   : Default
- [STATUS_XTRSP](#job-status-xtrsp) - XTRSP Status KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $30 Modus   : Default
- [STATUS_TRSP_DATEN](#job-status-trsp-daten) - aktuelle Transponder-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $40-$49 Modus   : Default
- [STATUS_SCHLUESSEL_FREI_GESPERRT](#job-status-schluessel-frei-gesperrt) - aktuelle Transponder-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $40-$49 Modus   : Default
- [STATUS_THS_HANDSENDER1](#job-status-ths-handsender1) - THS Handsender1 KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4A Modus   : Default
- [STATUS_THS_HANDSENDER2](#job-status-ths-handsender2) - THS Handsender1 KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4B Modus   : Default
- [STATUS_FBD_DATEN](#job-status-fbd-daten) - aktuelle Fernbedienung-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $50-$59 Modus   : Default
- [STATUS_HS_DATEN](#job-status-hs-daten) - aktuelle Handsender-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5A-$5B Modus   : Default
- [STATUS_FBD_UBAT](#job-status-fbd-ubat) - aktueller Status "UBat" aller FBDs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5C Modus   : Default
- [STATUS_HS_UBAT](#job-status-hs-ubat) - aktueller Status "UBat" aller HSs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5D Modus   : Default
- [STATUS_FBD_FELDSTAERKE](#job-status-fbd-feldstaerke) - aktueller Status "Feldstaerke" der FBDs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5E Modus   : Default
- [STATUS_WUP](#job-status-wup) - aktueller Status "Wake-Up-Pattern" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5F Modus   : Default
- [STATUS_FBD_PERSONALISIERUNG](#job-status-fbd-personalisierung) - aktueller Status "Personalisierung" der FBDs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $60 Modus   : Default
- [STATUS_FERTIG_TRANSP_WERKST](#job-status-fertig-transp-werkst) - 1 Byte lesen: "Fertigung/Transport/Werkstatt-MODE" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$100A Modus  : Default
- [STATUS_VEHICLE_PRODUCTION_DATE](#job-status-vehicle-production-date) - 8 ASCII Byte Production Date KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1009 Modus   : Default
- [STATUS_REPEAT_TABLE](#job-status-repeat-table) - 8 Byte Repeat Table Version KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x100D Modus   : Default
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - 17 ASCII Byte Fahrgestell-Nummer KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1010 Modus   : Default
- [STATUS_HO_CODE](#job-status-ho-code) - 8 Byte "HO-Codierung" lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1013 Modus  :  Default
- [STATUS_FZG_ZUSTAND](#job-status-fzg-zustand) - 14 Byte "Fahrzeug-Zustand" lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1015 Modus  :  Default
- [STATUS_FZG_TYP](#job-status-fzg-typ) - 11 Byte "Fahrzeug-Type" lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1011 Modus  :  Default
- [STATUS_BOS_CC_DATEN](#job-status-bos-cc-daten) - Lesen von 32 Byte "BOS_CC-Daten" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1016-1018 Modus   : Default
- [STATUS_FSD_DATEN](#job-status-fsd-daten) - Lesen von 32 Byte "FSD-Daten" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1019-101A Modus   : Default
- [STATUS_FAHRZEUGAUFTRAG](#job-status-fahrzeugauftrag) - Liest 16 Byte "Fahrzeugauftrag" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=3F00...3F13 Modus   : Default
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default
- [STEUERN_CAS_DIAGNOSE](#job-steuern-cas-diagnose) - Schreibt 6 Byte "Digital Outputs" KWP2000: $30 InputOutputControlByLocalIdentifier LocalIdentifier=$02 $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ISN](#job-steuern-isn) - Schreibt  4Byte "ISN" und kopiert diesen auf beide  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $01 Modus  : Default
- [STEUERN_MECH_SCHLUESSELCODE](#job-steuern-mech-schluesselcode) - Schreibt 10 Byte "mechan. Schluessel-Code"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $02 Modus  : Default
- [STEUERN_SCHLUESSEL_FREQUENZ](#job-steuern-schluessel-frequenz) - Schreibt 1 Byte "Schluessel-Frequenz"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $03 Modus  : Default
- [STEUERN_PROG_LOCATION_DATUM](#job-steuern-prog-location-datum) - Schreibt 3 Byte "Programmier-Ort/Datum"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $04 Modus  : Default
- [STEUERN_ZV_AUTHENTISIERUNG](#job-steuern-zv-authentisierung) - Schreibt 4 Byte "ZV-Authentisierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $05 Modus  : Default
- [STEUERN_ELV_AUTHENTISIERUNG](#job-steuern-elv-authentisierung) - Schreibt 4 Byte "ELV-Authentisierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $05 Modus  : Default
- [STEUERN_TRANSPONDERKENNUNG](#job-steuern-transponderkennung) - Schreibt 3 Byte "Transponder-Aktivierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $06 Modus  : Default
- [STEUERN_TRSP_FAHRZYKLUSZAEHLER](#job-steuern-trsp-fahrzykluszaehler) - Schreibt 4 Byte "Transponder-Fahrzykluszaehler"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $07 Modus  : Default
- [STEUERN_CAS_INIT_KENNUNG](#job-steuern-cas-init-kennung) - Schreibt 3 Byte "Initialisierungs-Kennung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $08 Modus  : Default
- [STEUERN_BDM_SPERREN](#job-steuern-bdm-sperren) - BDM Sperren (only in special mode with BDM interface!!!)  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $09 Modus  : Default
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$C001 Modus  : Default
- [STEUERN_EWS4_KEY](#job-steuern-ews4-key) - Schreibt 64 Byte EWS key  KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$C000 Modus  : Default
- [STEUERN_DME_RINGBUFFER](#job-steuern-dme-ringbuffer) - Schreibt 31 Byte "DME-Ringpuffer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0A Modus  : Default
- [STEUERN_ZVFH_RINGBUFFER](#job-steuern-zvfh-ringbuffer) - Schreibt 64+1 Byte "ZV/FH-Ringpuffer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0B Modus  : Default
- [STEUERN_ICT_BYTE](#job-steuern-ict-byte) - Internal Circuit Byte Schreiben  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0E Modus  : Default
- [STEUERN_SCHLUESSELDATEN](#job-steuern-schluesseldaten) - Schreibt 17 Byte "Schluessel-Daten"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $10...$19 Modus  : Default
- [STEUERN_SCHLUESSEL_GESPERRT](#job-steuern-schluessel-gesperrt) - Schreibt 1 Byte "Schluessel-Sperre"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $20 Modus  : Default
- [STEUERN_SCHLUESSEL_FREIGEBEN](#job-steuern-schluessel-freigeben) - Schreibt 1 Byte "Schluessel-Nummer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $21 Modus  : Default
- [AKTUALISIEREN_CHIP_CARD_DATEN](#job-aktualisieren-chip-card-daten) - Schreibt 1 Byte  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $23 Modus  : Default
- [STEUERN_BASESTATION](#job-steuern-basestation) - Schreibt 5 Byte "Basestation-Vorgabewerte"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $26 Modus  : Default
- [STEUERN_KOMMUNIKATION_PARAMETER](#job-steuern-kommunikation-parameter) - Schreibt 1 Byte "Kommunikation Parameter"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $28 Modus  : Default
- [STEUERN_CMD_READ_PAGE_TRSP](#job-steuern-cmd-read-page-trsp) - Schreibt 1 Byte "Transponder Page"  KWP 2000: $3B WriteDataByLocalIdentifier LocalIdentifier $29 Modus   : Default
- [STEUERN_ADR_XTRSP](#job-steuern-adr-xtrsp) - Schreibt 4 Byte "XTRSP-Adresse"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $2B Modus  : Default
- [STEUERN_PAGE_TRSP](#job-steuern-page-trsp) - Schreibt 5 Byte "TRSP-Page"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $2C Modus  : Default
- [STEUERN_SEQUENCE_COUNTER_XTRSP](#job-steuern-sequence-counter-xtrsp) - Schreibt 4 Byte "XTRSP, Sequ.-Counter"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $2E Modus  : Default
- [STEUERN_FBD_DATEN](#job-steuern-fbd-daten) - Schreibt 15 Byte "Daten fuer eine FBD" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $50-$59 Modus  : Default
- [STEUERN_FBD_UBAT](#job-steuern-fbd-ubat) - Schreibt 10 Byte "UBAT fuer alle FBD" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5C Modus:   Default
- [STEUERN_HS_UBAT](#job-steuern-hs-ubat) - Schreibt 2 Byte "UBAT fuer alle HS" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5D Modus:   Default
- [STEUERN_FBD_FELDSTAERKE](#job-steuern-fbd-feldstaerke) - Schreibt 6 Byte "FBD-Feldstaerke" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5E Modus:   Default
- [STEUERN_WUP](#job-steuern-wup) - Schreibt 3 Byte "Wake-Up-Pattern"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5F Modus  : Default
- [STEUERN_FBD_PERSONALISIERUNG](#job-steuern-fbd-personalisierung) - Schreibt 10 Byte "FBD Personalisierung Daten"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $60 Modus  : Default
- [STEUERN_VEHICLE_PRODUCTION_DATE](#job-steuern-vehicle-production-date) - 8 ASCII "Vehicle Production Date" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1009 Full Vehicle Identification Number Modus  : Default
- [STEUERN_FAHRGESTELLNUMMER](#job-steuern-fahrgestellnummer) - 17 ASCII "Fahrgestellnummer" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1010 Full Vehicle Identification Number Modus  : Default
- [STEUERN_HO_CODE](#job-steuern-ho-code) - 8 Byte "HO-Codierung" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1013 Modus  : Default
- [STEUERN_FAHRZEUGAUFTRAG](#job-steuern-fahrzeugauftrag) - Schreibt 16 Byte "Fahrzeugauftrag" KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=3F00...3F13 Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [SET_FERTIG_TRANSP_WERKST](#job-set-fertig-transp-werkst) - Initialisiert den Fertigung/Transport/Werkstatt-MODE KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $0C Modus  : Default
- [DME_STARTWERT_ABGLEICH](#job-dme-startwert-abgleich) - Kopiert die ISN auf beide Wechselcodes KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $20 Modus  : Default
- [SET_KEY_MODE](#job-set-key-mode) - 1 Byte =&gt; Command 0/1/2/3/-/5/6/7 11 Byte =&gt; Command -/-/-/-/4/-/-/- Startet einen KEY_MODE Befehl KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $21 Modus  : Default
- [SET_KEY_INIT](#job-set-key-init) - Initialisiert den KEY-MODE KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $22 Modus  : Default
- [SIGNATURPRUEFUNG](#job-signaturpruefung) - Aktiviert die Signaturpruefung des Flash-ROM KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $23 Modus  : Default
- [C_C_AUFTRAG_CAS](#job-c-c-auftrag-cas) - Codierd schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default
- [C_C_LESEN_CAS](#job-c-c-lesen-cas) - Codierd lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default
- [C_C_SCHREIBEN_CAS](#job-c-c-schreiben-cas) - Codierd schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default
- [ISTUFE_LESEN_CAS](#job-istufe-lesen-cas) - I_Stufe lesen KWP2000: $22   ReadDataByCommonIdentifier $100B Modus  : Default
- [ISTUFE_SCHREIBEN_CAS](#job-istufe-schreiben-cas) - I_Stufe schreiben KWP2000: $2E   WriteDataByCommonIdentifier $100B Modus  : Default
- [STATUS_CBS_VERSION](#job-status-cbs-version) - I_Stufe lesen KWP2000: $22   ReadDataByCommonIdentifier $1014 Modus  : Default
- [STEUERN_CBS_VERSION](#job-steuern-cbs-version) - I_Stufe schreiben KWP2000: $2E   WriteDataByCommonIdentifier $1014 Modus  : Default
- [SDIAG](#job-sdiag) - Universaler Diagnosebefehl Speziell fuer Tools SDIAG vom SIEMENS VDO Regensburg entwickelt KWP2000: $XX Modus  : Default
- [STATUS_CC_DATEN_ARG](#job-status-cc-daten-arg) - Lesen von 32 Byte "CC-Daten" KWP 2000: $31 StartRoutineByLocaldentifier $25 READ_CC_DATEN_ARG Local=0x00 - 0x19 Modus   : Default
- [ELV_IDENT](#job-elv-ident) - KWP 2000: $21 ReadDataByLocaldentifier Local=$05 Modus   : Default
- [STATUS_FNDCOM](#job-status-fndcom) - 3 Byte des EEPROM FNDCOM_Id Block KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $61 Modus   : Default
- [STEUERN_FNDCOM](#job-steuern-fndcom) - Schreibt  3Byte im EEPROM-Block FNDCOM_Id  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $61 Modus  : Default
- [STATUS_AUTHENT_FNDCOM](#job-status-authent-fndcom) - 1 Byte des Authentisierung des FNDCOM KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $62 Modus   : Default
- [STEUERN_FNDCOM_ANLERNEN](#job-steuern-fndcom-anlernen) - KWP2000: $31 StartRoutineByLID LocalIdentifier $26 00 XX Modus  : Default
- [STATUS_FNDCOM_FUNKTION](#job-status-fndcom-funktion) - KWP2000: $31 StartRoutineByLID LocalIdentifier $26 00 XX Modus  : Default
- [STATUS_RDU](#job-status-rdu) - Infospeicher lesen (alle Info-Meldungen) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory Infospeicher lesen detail (hier 0x9810) KWP2000: $22 ReadDataByCommonIdentifier $20XX dtcShadowMemoryEntry, wobei XX = Ort des RDU-INFO-Eintrags Liest Datum/Urzeit zum INFO_Eintrags 0x9810 KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $27
- [STATUS_ELV_WERTE](#job-status-elv-werte) - KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $7A Modus   : Default
- [STEUERN_ELVCOUNTER_CAS_LOESCHEN](#job-steuern-elvcounter-cas-loeschen) - Loeschen EscapeCounter von CAS KWP 2000: $21 $3B ReadWriteDataByLocalIdentifier LocalIdentifier $79 Modus   : Default
- [STEUERN_ELVCOUNTER_ELV_LOESCHEN](#job-steuern-elvcounter-elv-loeschen) - Loeschen EscapeCounter von ELV KWP 2000: $21 $3B ReadWriteDataByLocalIdentifier LocalIdentifier $79 Modus   : Default

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

<a id="job-sg-variante-lesen"></a>
### SG_VARIANTE_LESEN

Auslesen der SG-Variante auf Basis des Jobs Hardware Referenz lesen KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SG_VARIANTE | string | SG-Variante: PA ja/nein, RL/LL |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-status-cas-diagnose"></a>
### STATUS_CAS_DIAGNOSE

All Inputs Read KWP2000: $30 InputOutputControlByLocalIdentifier LocalIdentifier=0x01 $01 ReportCurrentState Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_INITDONE_CAS | unsigned char | Bereich 0/1 Byte00, Bit0 |
| STATUS_INITDONE_TRSP | unsigned char | Bereich 0/1 Byte00, Bit1 |
| STATUS_CRC_EEPROM | unsigned char | Bereich 0/1 Byte00, Bit2 |
| STATUS_CRC_FLASH | unsigned char | Bereich 0/1 Byte00, Bit3 |
| STATUS_MONTAGEMODE_KL15ELV | unsigned char | Status Montagemode KL15/ELV (0 deaktiv, 1 aktiv) Bereich 0/1 Byte00, Bit4 |
| STATUS_MONTAGEMODE_KL50 | unsigned char | Status Montagemode KL50 (0 deaktiv, 1 aktiv) Bereich 0/1 Byte00, Bit5 |
| STATUS_RESERVE_BYTE00_BIT6 | unsigned char | Bereich 0/1 Byte00, Bit6 |
| STATUS_LAYOUT_CAS2 | unsigned char | Bereich 0=E65CAS 1=CAS2 Byte00, Bit7 |
| IN_ZAS_SSTADISC | unsigned char | Bereich 0/1 Byte01, Bit0 |
| IN_ZAS_EJECTDISC | unsigned char | Bereich 0/1 Byte01, Bit1 |
| IN_ZAS_SSTBDISC | unsigned char | Bereich 0/1 Byte01, Bit2 |
| IN_ZAS_RASTDISC | unsigned char | Bereich 0/1 Byte01, Bit3 |
| IN_RCGLIED_DISC | unsigned char | Bereich 0/1 Byte01, Bit4 |
| IN_DFAHL_DISC | unsigned char | Bereich 0/1 Byte01, Bit5 |
| IN_DFAHLABRISS_DISC | unsigned char | Bereich 0/1 Byte01, Bit6 |
| IN_VKL3KMH_DISC | unsigned char | Bereich 0/1 Byte01, Bit7 |
| IN_BLS_DISC | unsigned char | Bereich 0/1 Byte02, Bit0 |
| IN_PK_DISC | unsigned char | Bereich 0/1 Byte02, Bit1 |
| IN_HKL_DISC | unsigned char | Bereich 0/1 Byte02, Bit2 |
| IN_TCU_DISC | unsigned char | Bereich 0/1 Byte02, Bit3 |
| IN_CLT_DISC | unsigned char | Bereich 0/1 Byte02, Bit4 |
| IN_MFS_DISC | unsigned char | Bereich 0/1 Byte02, Bit5 |
| IN_MHK_DISC | unsigned char | Bereich 0/1 Byte02, Bit6 |
| IN_KSTART_DISC | unsigned char | Bereich 0/1 Byte02, Bit7 |
| IN_HTL_DISC | unsigned char | Bereich 0/1 Byte03, Bit0 |
| IN_PLOCK_DISC | unsigned char | Bereich 0/1 Byte03, Bit1 |
| IN_LG_DISC | unsigned char | Bereich 0/1 Byte03, Bit2 |
| IN_WD_DIAGDISC | unsigned char | Bereich 0/1 Byte03, Bit3 |
| IN_BIMAG_STATUSDISC | unsigned char | Bereich 0/1 Byte03, Bit4 |
| IN_LED_DIAGDISC | unsigned char | Bereich 0/1 Byte03, Bit5 |
| IN_ELVHW_DIAGDISC | unsigned char | Bereich 0/1 Byte03, Bit6 |
| IN_ELVL2_DIAGDISC | unsigned char | Bereich 0/1 Byte03, Bit7 |
| IN_KL3KMH_DELAYDISC | unsigned char | Bereich 0/1 Byte04, Bit0 |
| IN_SCAN_NERRDISC | unsigned char | Bereich 0/1 Byte04, Bit1 |
| IN_KBUS_RXDDISC | unsigned char | Bereich 0/1 Byte04, Bit2 |
| IN_FBD_DATADISC | unsigned char | Bereich 0/1 Byte04, Bit3 |
| IN_TRSP_DATADISC | unsigned char | Bereich 0/1 Byte04, Bit4 |
| IN_EWS_DIAGDISC | unsigned char | Bereich 0/1 Byte04, Bit5 |
| IN_KL30X_DIAGDISC | unsigned char | Bereich 0/1 Byte04, Bit6 |
| IN_R_MRS_DIAGDISC | unsigned char | Bereich 0/1 Byte04, Bit7 |
| IN_KL30L_DIAGDISC | real | Einheit: Volt Byte05 |
| IN_KL30E_DIAGDISC | real | Einheit: Volt Byte06 |
| IN_ZASHALL12_DIAGDISC | real | Einheit: Volt Byte07 |
| IN_ZASHALL34_DIAGDISC | real | Einheit: Volt Byte08 |
| IN_ELVH_DIAGDISC | real | Einheit: Volt Byte09 |
| IN_ELVL_DIAGDISC | real | Einheit: Volt Byte10 |
| IN_KL30G_DIAGDISC | real | Einheit: Volt Byte11 |
| IN_KL15WUPRS_DIAGDISC | real | Einheit: Volt Byte12 |
| IN_KLR_DIAGDISC | real | Einheit: Volt Byte13 |
| IN_KL15_1DIAGDISC | real | Einheit: Volt Byte14 |
| IN_KL15_2DIAGDISC | real | Einheit: Volt Byte15 |
| IN_KL15_3DIAGDISC | real | Einheit: Volt Byte16 |
| IN_KL15WUP_DIAGDISC | real | Einheit: Volt Byte17 |
| IN_KL50L_DIAGDISC | real | Einheit: Volt Byte18 |
| IN_KL50RS_DIAGDISC | real | Einheit: Volt Byte19 |
| IN_KL50_STROMDISC | real | Einheit: Ampere Byte20 |
| STAT_NWM4 | unsigned char | Bereich 0-255 Byte21 |
| STAT_NWM5 | unsigned char | Bereich 0-255 Byte22 |
| STAT_NWM6 | unsigned char | Bereich 0-255 Byte23 |
| STAT_NWM7 | unsigned char | Bereich 0-255 Byte24 |
| KEY_STATUS_0 | unsigned char | Bereich 0..255 Byte25 |
| KEY_STATUS_1 | unsigned char | Bereich 0..255 Byte26 |
| KEY_STATUS_2 | unsigned char | Bereich 0..255 Byte27 |
| KEY_STATUS_3 | unsigned char | Bereich 0..255 Byte28 |
| KEY_STATUS_4 | unsigned char | Bereich 0..255 Byte29 |
| KEY_STATUS_5 | unsigned char | Bereich 0..255 Byte30 |
| STAT_KEY_NO_IDENTIFIER | unsigned char | Bereich 0/1 Byte26, Bit5 |
| STAT_KEY_WRONG_FREQUENCY | unsigned char | Bereich 0/1 Byte29, Bit3 |
| STAT_KEY_WRONG_MECH_CODE | unsigned char | Bereich 0/1 Byte29, Bit5 |
| STAT_KEY_NO_POCKET_KEY | unsigned char | Bereich 0/1 Byte29, Bit6 |
| STAT_KEY_NO_FBD_PA_KEY | unsigned char | Bereich 0/1 Byte29, Bit7 |
| FBD_QUELLE | unsigned char | Bereich 0..255 Byte31 |
| FBD_PERSONAL_NR | unsigned char | Bereich 0..255 Byte32 |
| FBD_KEY_NR | unsigned char | Bereich Byte33 |
| FBD_QUANT | unsigned char | Bereich 0-255 Byte34 |
| FBD_MFS_START | unsigned char | Bereich 0-255 Byte35 |
| FBD_MFS_STOPP | unsigned char | Bereich 0-255 Byte36 |
| PERIODE_DFASIM | unsigned int | Signal period_ms, Bereich 0-65535 Byte37-38 |
| KS_IO_BLS | unsigned char | Bereich 0-1 Byte39, Bit 0 |
| KS_IO_P | unsigned char | Bereich 0-1 Byte39, Bit 1 |
| KS_IO_CLUTCH | unsigned char | Bereich 0-1 Byte39, Bit 2 |
| KS_IO_ENGINE | unsigned char | Bereich 0-1 Byte39, Bit 3 |
| KS_IO_SPEED | unsigned char | Bereich 0-1 Byte39, Bit 4 |
| KS_IO_EMERGENCY | unsigned char | Bereich 0-1 Byte39, Bit 5 |
| KS_IO_WITHDRAWL | unsigned char | Bereich 0-1 Byte39, Bit 6 |
| _KS_IO_MONTAGE | unsigned char | Bereich 0-1 Byte39, Bit 7 Bitte dieses Result nur noch Übergangsweise benutzen, wird in der nächsten Verion entfernt (maka040618) |
| KS_IO_DEBRAST | unsigned char | Bereich 0-1 Byte40, Bit 0 |
| KS_IO_DEBEJECT | unsigned char | Bereich 0-1 Byte40, Bit 1 |
| KS_IO_DEBSSTB | unsigned char | Bereich 0-1 Byte40, Bit 2 |
| KS_IO_DEBSSTA | unsigned char | Bereich 0-1 Byte40, Bit 3 |
| KS_IO_HALLERROR | unsigned char | Bereich 0-1 Byte40, Bit 4 |
| KS_IO_STATECHANGE | unsigned char | Bereich 0-1 Byte40, Bit 5 |
| KS_IO_ELVACCESS | unsigned char | Bereich 0-1 Byte40, Bit 6 |
| KS_IO_KEYACCESS | unsigned char | Bereich 0-1 Byte40, Bit 7 |
| KS_SM_DIAGKL0 | unsigned char | Bereich 0-15 Byte41, Bit 0-3 |
| KS_SM_DIAGKLR | unsigned char | Bereich 0-15 Byte41, Bit 4-7 |
| KS_SM_DIAGKL15 | unsigned char | Bereich 0-15 Byte42, Bit 0-3 |
| KS_SM_DIAGKL50 | unsigned char | Bereich 0-15 Byte42, Bit 4-7 |
| KS_DRV_KSLED | unsigned char | Bereich 0-15 Byte43, Bit 0 |
| KS_DRV_KSBIMAG | unsigned char | Bereich 0-15 Byte43, Bit 1 |
| KS_DRV_KSVCCHALL | unsigned char | Bereich 0-15 Byte43, Bit 2 |
| KS_DRV_KSKL30G | unsigned char | Bereich 0-15 Byte43, Bit 3 |
| KS_DRV_KSKLR | unsigned char | Bereich 0-15 Byte43, Bit 4 |
| KS_DRV_KSKL15123 | unsigned char | Bereich 0-15 Byte43, Bit 5 |
| KS_DRV_KSKL15WUP | unsigned char | Bereich 0-15 Byte43, Bit 6 |
| KS_DRV_KSKL50 | unsigned char | Bereich 0-15 Byte43, Bit 7 |
| KS_ANL_SPERRE | unsigned char | Bereich 0/1 Byte43, Bit 0 |
| KS_WATCHDOG | unsigned char | Bereich 0/1 Byte43, Bit 1 |
| KS_BIMAG_POSITION | unsigned char | Bereich 0-15 Byte43, Bit 2 |
| KS_STATE_TERMINAL | unsigned char | Bereich 0-15 Byte43, Bit 3 |
| S_PE_KAPFAT | unsigned char | Bereich 0-1 Byte45, Bit 0 |
| S_PE_KAPFATH | unsigned char | Bereich 0-1 Byte45, Bit 1 |
| S_PE_KAPBFT | unsigned char | Bereich 0-1 Byte45, Bit 2 |
| S_PE_KAPBFTH | unsigned char | Bereich 0-1 Byte45, Bit 3 |
| S_PE_ERFAT | unsigned char | Bereich 0-1 Byte45, Bit 4 |
| S_PE_ERFATH | unsigned char | Bereich 0-1 Byte45, Bit 5 |
| S_PE_ERBFT | unsigned char | Bereich 0-1 Byte45,Bit 6 |
| S_PE_ERBFTH | unsigned char | Bereich 0-1 Byte45, Bit 7 |
| S_PE_VRFAT | unsigned char | Bereich 0-1 Byte46, Bit 0 |
| S_PE_VRFATH | unsigned char | Bereich 0-1 Byte46, Bit 1 |
| S_PE_VRBFT | unsigned char | Bereich 0-1 Byte46, Bit 2 |
| S_PE_VRBFTH | unsigned char | Bereich 0-1 Byte46,Bit 3 |
| S_PA_IDGPRIO | unsigned char | Bereich 0-15 Byte46, Bit 4-7 |
| S_PE_FT_AUTH | unsigned char | Bereich 0-1 Byte47,Bit 0 |
| S_PE_FTH_AUTH | unsigned char | Bereich 0-1 Byte47,Bit 1 |
| S_PE_BFT_AUTH | unsigned char | Bereich 0-1 Byte47,Bit 2 |
| S_PE_BFTH_AUTH | unsigned char | Bereich 0-1 Byte47,Bit 3 |
| S_PE_HK_AUTH | unsigned char | Bereich 0-1 Byte47,Bit 4 |
| S_PE_ER | unsigned char | Bereich 0-1 Byte47,Bit 5 |
| S_PE_VR | unsigned char | Bereich 0-1 Byte47,Bit 6 |
| Z_PA_TRSP | unsigned char | Bereich 0-1 Byte47,Bit 7 |
| S_PE_STATE | unsigned char | Bereich 0-255 Byte48 |
| S_PG_STATE | unsigned char | Bereich 0-255 Byte49 |
| S_HK_STATE | unsigned char | Bereich 0-255 Byte50 |
| S_AUTH_STATE | unsigned char | Bereich 0-255 Byte51 |
| S_SEARCH_STATE | unsigned char | Bereich 0-255 Byte52 |
| STAT_KL_R | unsigned char | Status_Klemme_R (00=Kl R aus,01=Kl R ein), Bereich 0-3 Byte53, Bit 0-1 |
| STAT_KL_15 | unsigned char | Status_Klemme_15 (00=Kl 15 aus,01=Kl 15 ein), Bereich 0-3 Byte53, Bit 2-3 |
| STAT_KL_50 | unsigned char | Status_Klemme_50 (00=Kl 50 aus,01=Kl 50 ein), Bereich 0-3 Byte53, Bit 4-5 |
| STAT_KEY_VALID | unsigned char | Status_Schlüssel_Gueltig (00=no key,01=valid key,10=no valid key), Bereich 0-3 Byte53, Bit 6-7 |
| NO_KEY | unsigned char | Schluesselnummer, Bereich 0-15 Byte54, Bit 0-3 |
| STAT_KEY_TYP | unsigned char | Status_Schluessel_Typ (0=no key,2=Pocket,4=Remote,5=PA), Bereich 0-15 Byte54, Bit 4-7 |
| STAT_KEY_PLGD | unsigned char | Status_Schluessel_Steckt (00=no key,01=key plugged), Bereich 0-3 Byte55, Bit 0-1 |
| STAT_VHIM | unsigned char | Status_Wegfahrsperre (01=gesperrt,10=frei), Bereich 0-3 Byte55, Bit 2-3 |
| STAT_LOKG_STCO | unsigned char | Bereich 0-3 Byte55, Bit 4-5 |
| STAT_KEYLOCK | unsigned char | Status_Keylock (00=not active,01=active), Bereich 0-3 Byte55, Bit 6-7 |
| POS_ID_PU | unsigned char | Position_ID_Geber (00=Kein IDG,01=IDG im Innenraum,10=IDG ausserhalb erkannt), Bereich 0-3 Byte56, Bit 0-1 |
| STAT_PSVA_ACV | unsigned char | Status_Passive-Access_Aktiv (00=not active,01=active), Bereich 0-3 Byte56, Bit 2-3 |
| CTR_ENG_RMST_EGS | unsigned char | Bereich 0-3 Byte56, Bit 4-5 |
| STAT_KL_15_HW | unsigned char | Status_Klemme_15HW (00=Kl15 aus,01=Kl15-3 kein KS oder SST, 02=KL15 kein KS), Bereich 0-3 Byte56, Bit 6-7 |
| ALIV_KL | unsigned char | Alive_Klemme, Bereich 0-15 Byte57, Bit 0-3 |
| CHKSM_KL | unsigned char | Checksumme_Klemme, Bereich 0-15 Byte57, Bit 4-7 |
| STAT_CLSY | unsigned char | Status_Zentralverriegelung (s. LH), Bereich 0-15 Byte58, Bit 0-3 |
| CTR_CLSY | unsigned char | Steuerung_Zentralverriegelung (s. LH), Bereich 0-15 Byte58, Bit 4-7 |
| STAT_DSW_DRD | unsigned char | Status_Tuerkontakt_FAT (00=geschlossen,01=offen), Bereich 0-3 Byte59, Bit 0-1 |
| STAT_DSW_PSD | unsigned char | Status_Tuerkontakt_BFT (00=geschlossen,01=offen), Bereich 0-3 Byte59, Bit 2-3 |
| STAT_DSW_DVDR | unsigned char | Status_Tuerkontakt_FATH (00=geschlossen,01=offen), Bereich 0-3 Byte59, Bit 4-5 |
| STAT_DSW_PSDR | unsigned char | Status_Tuerkontakt_BFTH (00=geschlossen,01=offen), Bereich 0-3 Byte59, Bit 6-7 |
| STAT_CT_BTL | unsigned char | Status_Kontakt_Heckklappe (00=geschlossen,01=offen), Bereich 0-3 Byte60, Bit 0-1 |
| STAT_CT_BON | unsigned char | Status_Kontakt_Motorhaube (00=geschlossen,01=offen), Bereich 0-3 Byte60, Bit 2-3 |
| STAT_HOTM | unsigned char | Status_Hotelstellung (00=nicht aktiv,01=aktiv), Bereich 0-3 Byte60, Bit 4-5 |
| STAT_PUBU_CLSY | unsigned char | Status_Taster_Zentralverriegelung (00= nicht betaetigt,01=entriegeln,10=verriegeln), Bereich 0-3 Byte60, Bit 6-7 |
| STAT_DREHZAHL_MOTOR | unsigned int | Bereich 0-65535 Signal RPM_ENGINE, Byte61-62 |
| STAT_GANG_GETRIEBE | unsigned char | Signal ST_GR_GRB, Bereich 0-15 (s. LH) Byte63 |
| STAT_KONTAKT_BREMSPEDAL | unsigned char | Signal ST_CT_BRPD, Bereich 0-3 (s. LH) Byte63 |
| STAT_MOTOR_LAEUFT | unsigned char | Signal ST_ENG_RUN, Bereich 0-3 (s. LH) Byte63 |
| IN_VGR3KMH_DISC | unsigned char | Bereich 0/1 Byte01, Bit6 |
| IN_ER_DISC | unsigned char | Bereich 0/1 Byte02, Bit2 |
| IN_VR_DISC | unsigned char | Bereich 0/1 Byte02, Bit3 |
| IN_RESERVE1_DISC | unsigned char | Bereich 0/1 Byte03, Bit1 |
| IN_PCAN_NERRDISC | unsigned char | Bereich 0/1 Byte03, Bit2 |
| RESERVE_BYTE03_BIT7 | unsigned char | Bereich 0/1 Byte03, Bit7 |
| STATUS_RING_DATA_3 | unsigned char | Bereich 0-255 Byte04 |
| IN_KL15_4DIAGDISC | real | Einheit: Volt Byte10 |
| FBD_QUANT_MAX | unsigned char | Bereich 0-255 Byte25 |
| FBD_QUANT_MIN | unsigned char | Bereich 0-255 Byte26 |
| STAT_RADDREHZAHL | unsigned int | Signal STATE_DFAHL, Bereich 0-65535 Byte28-29 |
| ZAS_BEDIENSPERRE | unsigned char | Bereich 0-1 Byte30, Bit 0 |
| ZAS_SSTAB | unsigned char | Bereich 0-1 Byte30, Bit 1 |
| ZAS_SST | unsigned char | Bereich 0-1 Byte30, Bit 2 |
| ZAS_EJECT | unsigned char | Bereich 0-1 Byte30, Bit 3 |
| ZAS_FLANKE | unsigned char | Bereich 0-1 Byte30, Bit 4 |
| ZAS_NOTAUS | unsigned char | Bereich 0-1 Byte30, Bit 5 |
| ZAS_KOMFORTAUS | unsigned char | Bereich 0-1 Byte30, Bit 6 |
| ZAS_VERRASTET | unsigned char | Bereich 0-1 Byte30, Bit 7 |
| ZAS_ALSP | unsigned char | Bereich 0-1 Byte31, Bit 0 |
| ZAS_AWSP | unsigned char | Bereich 0-1 Byte31, Bit 1 |
| ZAS_AZSP | unsigned char | Bereich 0-1 Byte31, Bit 2 |
| ZAS_PDISC | unsigned char | Bereich 0-1 Byte31, Bit 3 |
| ZAS_NCAN | unsigned char | Bereich 0-1 Byte31, Bit 4 |
| ZAS_PCAN | unsigned char | Bereich 0-1 Byte31, Bit 5 |
| ZAS_NMOT | unsigned char | Bereich 0-1 Byte31, Bit 6 |
| ZAS_BLS | unsigned char | Bereich 0-1 Byte31, Bit 7 |
| ZAS_VFZGAZSP | unsigned char | Bereich 0-1 Byte32, Bit 0 |
| ZAS_VFZGNOTST | unsigned char | Bereich 0-1 Byte32, Bit 0 |
| ZAS_VFZGHW | unsigned char | Bereich 0-1 Byte32, Bit 2 |
| ZAS_FREIGABE | unsigned char | Bereich 0-1 Byte32, Bit 3 |
| ZAS_FERNSTART | unsigned char | Bereich 0-1 Byte32, Bit 4 |
| ZAS_SWRCGLFENSTER | unsigned char | Bereich 0-1 Byte32, Bit 5 |
| ZAS_PA_AKTIV | unsigned char | Bereich 0-1 Byte32, Bit 6 |
| ZAS_BLS_DEFEKT | unsigned char | Bereich 0-1 Byte32, Bit 7 |
| ZAS_CCM_SET | unsigned char | Bereich 0-1 Byte33, Bit 0 |
| ZAS_BHOFFEN | unsigned char | Bereich 0-1 Byte33, Bit 1 |
| ZAS_BHOFFEN_DTC | unsigned char | Bereich 0-1 Byte33, Bit 2 |
| ZAS_P_ALSP | unsigned char | Bereich 0-1 Byte33, Bit 3 |
| ZAS_P_AZSP | unsigned char | Bereich 0-1 Byte33, Bit 4 |
| ZAS_SIGNATUR_DUMMY1 | unsigned char | Bereich 0-3 Byte34 |
| ZAS_SIGNATUR_DUMMY2 | unsigned char | Bereich 0-255 Byte35 |
| ZAS_SIGNATUR_DUMMY3 | unsigned char | Bereich 0-255 Byte36 |
| AUTH_CLSY_0 | unsigned char | Authentisierung_Zentralverriegelung, Bereich 0-255 Byte53 |
| AUTH_CLSY_1 | unsigned char | Bereich 0-255 Byte54 |
| AUTH_CLSY_2 | unsigned char | Bereich 0-255 Byte55 |
| AUTH_CLSY_3 | unsigned char | Bereich 0-255 Byte56 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-isn"></a>
### STATUS_ISN

4 Byte des ISN KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $01 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mechanischer-schluesselcode"></a>
### STATUS_MECHANISCHER_SCHLUESSELCODE

5 Byte des Mechanischer Schluesselcode KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $02 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSELCODE | string | ausgelesene Mechanischer Schluesselcode |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schluessel-frequenz"></a>
### STATUS_SCHLUESSEL_FREQUENZ

Frequenz des Schluessels KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $03 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KEY_FREQ | unsigned char |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-prog-location-datum"></a>
### STATUS_PROG_LOCATION_DATUM

Ort und Datum der ECU-Programmierung KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $04 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROG_LOCATION | unsigned char | "Ort":   0-15 Byte0,Bit4-7 |
| PROG_TIME_MONTH | unsigned char | "Monat": 1-12 Byte0,Bit0-3 |
| PROG_TIME_DAY | unsigned int | "Tag":   1-31 Byte1 |
| PROG_TIME_YEAR_2_DIGITS | unsigned char | "Jahr":  0-99 Byte2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zv-authentisierung"></a>
### STATUS_ZV_AUTHENTISIERUNG

aktueller Status "ZV-Authentisierung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $05 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZV_AUTHENT | binary | 4 Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-elv-authentisierung"></a>
### STATUS_ELV_AUTHENTISIERUNG

aktueller Status "ELV-Authentisierung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $05 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ELV_AUTHENT | binary | 4 Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trsp-init"></a>
### STATUS_TRSP_INIT

aktueller Status "TRSP, Init-Kennung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $06 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TRSP_INIT | binary | 3 Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trsp-fahrzykluszaehler"></a>
### STATUS_TRSP_FAHRZYKLUSZAEHLER

aktueller Status "TRSP, Fahrzykluszaehler" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $07 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZAEHLER_HIGH_WORD | unsigned int | ======&gt; Byte0-1 |
| ZAEHLER_LOW_WORD | unsigned int | ======&gt; Byte2-3 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cas-init-kennung"></a>
### STATUS_CAS_INIT_KENNUNG

aktueller Status "CAS, Init-Kennung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $08 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CAS_INIT | binary | 3 Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bdm-sperren"></a>
### STATUS_BDM_SPERREN

BDM-Sperren-Status Lesen KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $09 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_BDM | unsigned char | 0xFF-offen 0xAA-sperren |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews"></a>
### STATUS_EWS

aktueller Status "EWS4 key" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Modus   : Default Zurücklesen verschiedener interner Stati für EWS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS3_CAPABLE | int | 0 Das SG beherrscht kein EWS3 1 Das SG beherrscht EWS3 |
| STAT_EWS4_CAPABLE | int | 0 Das SG beherrscht kein EWS4 1 Das SG beherrscht EWS4 |
| STAT_EWS3_ACTIVE | int | 0 EWS3 ist nicht (mehr) aktiv 1 EWS3 ist aktiv (oder lässt sich aktivieren) |
| STAT_EWS4_ACTIVE | int | 0 EWS4 ist nicht aktiv 1 EWS4 ist aktiv |
| STAT_EWS_EGS_ACTIVE | int | 0 EWS-EGS inaktiv 1 EWS-EGS aktiv |
| STAT_EWS4_SERVER_SK_LOCKED | int | 0 SecretKey server lässt sich noch direkt schreiben 1 SecretKey server lässt sich nicht mehr schreiben/lesen |
| STAT_EWS4_SERVER_KEY | int | table EWS4_KEY_STATE WERT |
| STAT_EWS4_SERVER_KEY_TXT | string | table EWS4_KEY_STATE TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

aktueller Status "EWS4 secret keys" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Modus   : Default Lesen des SecretKey des Server (CAS) sowie Client (DME) für EWS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_SERVER_SK | binary | Secret key Server |
| STAT_EWS4_CLIENT_SK | binary | Secret key Client |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews4-key"></a>
### STATUS_EWS4_KEY

aktueller Status "EWS4 key" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EWS4_KEY | binary | 64 Byte Byte0-63 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dme-ringbuffer"></a>
### STATUS_DME_RINGBUFFER

aktueller Status "DME-RingBuffer" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0A Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DME_RINGBUFFER | binary | 30 Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zvfh-ringbuffer"></a>
### STATUS_ZVFH_RINGBUFFER

aktueller Status "ZV/FH-Ringpuffer" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0B Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BUFFER_POINTER | unsigned char | Byte0 |
| ZVFH_RINGBUFFER | binary | 64 Byte Byte1-64 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fbd-telegramm"></a>
### STATUS_FBD_TELEGRAMM

letztes FBD-Telegramm KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0C Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBD_TELEGRAMM | binary | 20 Byte Byte0-19 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pa-telegramm"></a>
### STATUS_PA_TELEGRAMM

letztes PA-Telegramm KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0D Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PA_TELEGRAMM | binary | 20 Byte Byte0-19 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ict-byte"></a>
### STATUS_ICT_BYTE

Internal Circuit Test Byte (Siemens Data) KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0E Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_ICT | unsigned char | 1 Byte Byte0 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mlfb"></a>
### STATUS_MLFB

MLFB Data Siemens KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0F Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MLFB_DATA | string | 8 Byte Byte0-7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schluessel-daten"></a>
### STATUS_SCHLUESSEL_DATEN

Auslesen der SCHLUESSELDATEN KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $10...$19 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_NUMMER | int | Werte: 1...10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_BYTE1 | unsigned char | Schluessel-Status-Byte1 |
| STATUS_BYTE2 | unsigned char | Schluessel-Status-Byte2 |
| INITIALISIERUNGSSTATUS | unsigned char | Initialisierungsstatus |
| IDENTIFIER | binary | Schluessel-Identifier, 4 Byte |
| SECRET_KEY | binary | Secret Key, 6 Byte |
| CONFIG_BYTE | unsigned char | Config-Byte |
| PASSWORD_TRANSPONDER | binary | Password Transponder, 3 Byte |
| CRC_BYTE | unsigned char | CyclicRedundancyCheck-Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schluessel-batteriezustand"></a>
### STATUS_SCHLUESSEL_BATTERIEZUSTAND

1 Byte KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $22 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_BATTERIEZUSTAND | int | ausgelesene Batteriezustand 0x0             - 2,6V &lt; Ubat 0x1             - 2,2V &lt; Ubat &lt; 2,6V 0x2             - Ubat &lt; 2,2V 0xFF    - Ubat unbekannt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-system-fehler-klstrg"></a>
### STATUS_SYSTEM_FEHLER_KLSTRG

1 Byte KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $24 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HALL_FEHLER | int | Bereich 0/1 Byte01, Bit0 |
| SCHUESSELPOSITION | int | Bereich 0-7 Byte01, Bit1-3 |
| FREIGABE_KEY | int | Bereich 0/1 Byte01, Bit4 |
| STARTABBRUCH_KL50 | int | Bereich 0/1 Byte03, Bit0 |
| ANLASSERSPERRE | int | Bereich 0/1 Byte03, Bit1 |
| ANLASSERSPERRE_BREMSE | int | Bereich 0/1 Byte03, Bit2 |
| ANLASSERSPERRE_KUPPLUNG | int | Bereich 0/1 Byte03, Bit3 |
| KURZSCHLUSS_BI_MAGNET | int | Bereich 0/1 Byte05, Bit0 |
| KURZSCHLUSS_HALL_SENSOREN | int | Bereich 0/1 Byte05, Bit1 |
| KURZSCHLUSS_KLR | int | Bereich 0/1 Byte05, Bit2 |
| KURZSCHLUSS_KL15 | int | Bereich 0/1 Byte05, Bit3 |
| KURZSCHLUSS_KL15WUP_RS | int | Bereich 0/1 Byte05, Bit4 |
| KURZSCHLUSS_KL50 | int | Bereich 0/1 Byte05, Bit5 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-basestation"></a>
### STATUS_BASESTATION

Auslesen der Basestation Status KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $25 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BASESTATION_PAGE0 | unsigned char | Basestation Page 0 |
| BASESTATION_PAGE1 | unsigned char | Basestation Page 1 |
| BASESTATION_PAGE2 | unsigned char | Basestation Page 2 |
| BASESTATION_PAGE3 | unsigned char | Basestation Page 3 |
| SAMPLING_TIME | unsigned char | Sampling Time |
| PHASE | unsigned char | Phase |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktuell-schluessel"></a>
### STATUS_AKTUELL_SCHLUESSEL

aktuelle Schluessel KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $27 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KEY_IS_IN_LOCK | unsigned char | Bereich 0/1 Byte0, Bit0 |
| KEY_IS_ENGAGED | unsigned char | Bereich 0/1 Byte0, Bit1 |
| KEY_IS_VALID | unsigned char | Bereich 0/1 Byte0, Bit2 |
| KEY_INVALID_AUTH | unsigned char | Bereich 0/1 Byte0, Bit3 |
| ID_PERMITTED_TRSP | unsigned char | Bereich 0/1 Byte0, Bit4 |
| KEY_WITH_TRSP_STARC | unsigned char | Bereich 0/1 Byte0, Bit5 |
| KEY_INVALID_TEMP | unsigned char | Bereich 0/1 Byte0, Bit6 |
| KEY_INIT_DIAG | unsigned char | Bereich 0/1 Byte0, Bit7 |
| ANT_BASE_NOT_OK | unsigned char | Bereich 0/1 Byte1, Bit0 |
| DEFAULT_AUTH | unsigned char | Bereich 0/1 Byte1, Bit1 |
| PAGE3_INVALID_CRYPT | unsigned char | Bereich 0/1 Byte1, Bit2 |
| EINTRAG_0 | unsigned char | Bereich 0/1 Byte1, Bit3 |
| RISC_INIT | unsigned char | Bereich 0/1 Byte1, Bit4 |
| TRSP_INIT | unsigned char | Bereich 0/1 Byte1, Bit5 |
| BACKUPKEY_INVALID | unsigned char | Bereich 0/1 Byte1, Bit6 |
| EE_INIT_DONE | unsigned char | Bereich 0/1 Byte1, Bit7 |
| KEY_USED | unsigned char | Bereich 0/1 Byte2, Bit0 |
| MEC_CODE_OK | unsigned char | Bereich 0/1 Byte2, Bit1 |
| MEC_CODE_NOT_TESTED | unsigned char | Bereich 0/1 Byte2, Bit2 |
| KEY_AUTOINIT | unsigned char | Bereich 0/1 Byte2, Bit3 |
| KEY_TYPE | unsigned char | Bereich 0/1 Byte2, Bit4/5/6 |
| ERC | unsigned char | Bereich 0/1 Byte2, Bit7 |
| KEY_NUMBER | unsigned char | Bereich: 0-9 Schluessel Byte3 |
| ID_NOT_SENT_BY_TRSP | unsigned char | Bereich 0/1 Byte4, Bit0 |
| NO_AUTH_WITH_CRYPT | unsigned char | Bereich 0/1 Byte4, Bit1 |
| PAGE_READ | unsigned char | Bereich 0/1 Byte4, Bit2 |
| PAGE_WRITE | unsigned char | Bereich 0/1 Byte4, Bit3 |
| KEY_DISABLED | unsigned char | Bereich 0/1 Byte4, Bit4 |
| ID_SENT_BUT_UNKNOWN | unsigned char | Bereich 0/1 Byte4, Bit5 |
| INIT_POS_0 | unsigned char | Bereich 0/1 Byte4, Bit6 |
| INIT_POS_1_TO_9 | unsigned char | Bereich 0/1 Byte4, Bit7 |
| INIT_BACKUPKEY | unsigned char | Bereich 0/1 Byte5, Bit0 |
| CC_AFTER_ACTIVE | unsigned char | Bereich 0/1 Byte5, Bit1 |
| CC_DATA_INIT | unsigned char | Bereich 0/1 Byte5, Bit2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-transponder-page"></a>
### STATUS_TRANSPONDER_PAGE

Transponder Page KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2A Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TRANSPONDER_PAGE | binary | Transponder Page |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-set-page-trsp"></a>
### STATUS_SET_PAGE_TRSP

Page TRSP KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2D Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TEST_FLAG | unsigned char | Test Data |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-xtrsp-test-data"></a>
### STATUS_XTRSP_TEST_DATA

Test Data KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2F Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TEST_DATA | unsigned long | Test Data |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-xtrsp"></a>
### STATUS_XTRSP

XTRSP Status KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $30 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_XTRSP_HI | unsigned int | XTRSP Status high |
| STAT_XTRSP_LO | unsigned int | XTRSP Status low |
| GUELTIGER_WERT | unsigned char | Bereich 0/1 |
| PROGRAMMIERUNG_FEHLERHAFT | unsigned char | Bereich 0/1 |
| R_W_SEQUENZ_NOCH_NICHT_BEENDET | unsigned char | Bereich 0/1 |
| CKS_FEHLER | unsigned char | Bereich 0/1 |
| ZUGRIFF_VERWEIGERT | unsigned char | Bereich 0/1 |
| FEHLERHAFTE_REIHENFOLGE | unsigned char | Bereich 0/1 |
| BLOCK_IST_ZUGRIFFSGESPERRT | unsigned char | Bereich 0/1 |
| BERECHNUNG_NOCH_NICHT_ABGESCHLOSSEN | unsigned char | Bereich 0/1 |
| INIT_MAL_ERFOLGT | unsigned char | Bereich 0/1 |
| INIT_GESPERRT | unsigned char | Bereich 0/1 |
| TOGGLE_BIT | unsigned char | Bereich 0/1 |
| BATTERIE_VOLL | unsigned char | Bereich 0/1 |
| PAGE | unsigned char | Page |
| BLOCK | unsigned char | Block |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trsp-daten"></a>
### STATUS_TRSP_DATEN

aktuelle Transponder-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $40-$49 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_NUMMER | int | Werte: 1...10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATE1 | unsigned char | Bereich Byte0, Bit0-7 |
| STATE2 | unsigned char | Byte1, Bit0-7 |
| STAT_INITIALISIERUNG | unsigned char | Bereich Byte2, Bit0-7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schluessel-frei-gesperrt"></a>
### STATUS_SCHLUESSEL_FREI_GESPERRT

aktuelle Transponder-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $40-$49 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KEY1 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY2 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY3 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY4 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY5 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY6 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY7 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY8 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY9 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| KEY10 | unsigned char | Bereich 0-freigeschalet, 1-gesperrt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ths-handsender1"></a>
### STATUS_THS_HANDSENDER1

THS Handsender1 KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4A Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| THS_HANDSENDER1 | binary | 2 Byte Byte0-1 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ths-handsender2"></a>
### STATUS_THS_HANDSENDER2

THS Handsender1 KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4B Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| THS_HANDSENDER2 | binary | 2 Byte Byte0-1 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fbd-daten"></a>
### STATUS_FBD_DATEN

aktuelle Fernbedienung-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $50-$59 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_NUMMER | int | Werte: 1...10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NUMBER_WORD | binary | Schluessel-Nr, Bereich: 0-65535 bzw. 0x0000-0xFFFF Byte0-1 |
| SECRET_KEY_HIGH | binary | Bereich: 0-65535 bzw. 0x0000-0xFFFF Byte2-3 |
| SECRET_KEY_LOW | binary | Bereich: 0x00000000-0xFFFFFFFF Byte4-7 |
| RANDOM_FBD | binary | Bereich: 0x00000000-0xFFFFFFFF Byte8-11 |
| LAUF_NR | unsigned char | Personalisierung Nummer Byte12 |
| UBAT_STAT | unsigned char | Hex-Antwort von SG Byte13, Bit0-7 |
| STAT_FBD | unsigned char | Bereich Byte14, Bit0-7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-daten"></a>
### STATUS_HS_DATEN

aktuelle Handsender-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5A-$5B Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HANDSENDER_NUMMER | int | Werte: 1...2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HS_HIGH | unsigned char | Handsender-Nr, Bit8-15 Byte0 |
| HS_LOW | unsigned char | Handsender-Nr, Bit0-7 Byte1 |
| SECRET_KEY_HIGH | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF Byte2-3 |
| SECRET_KEY_LOW | unsigned long | Bereich: 0x00000000-0xFFFFFFFF Byte4-7 |
| IDENTIFIER | unsigned long | Bereich: 0x00000000-0xFFFFFFFF Byte8-11 |
| RANDOM_FBD | unsigned long | Bereich: 0x00000000-0xFFFFFFFF Byte12-15 |
| UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte16, Bit0-2 |
| UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte16, Bit7 |
| STAT_HS | unsigned char | Bereich Byte17, Bit0-7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fbd-ubat"></a>
### STATUS_FBD_UBAT

aktueller Status "UBat" aller FBDs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5C Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBD01_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte0, Bit0-2 |
| FBD01_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte0, Bit7 |
| FBD02_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte1, Bit0-2 |
| FBD02_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte1, Bit7 |
| FBD03_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte2, Bit0-2 |
| FBD03_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte2, Bit7 |
| FBD04_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte3, Bit0-2 |
| FBD04_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte3, Bit7 |
| FBD05_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte4, Bit0-2 |
| FBD05_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte4, Bit7 |
| FBD06_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte5, Bit0-2 |
| FBD06_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte5, Bit7 |
| FBD07_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte6, Bit0-2 |
| FBD07_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte6, Bit7 |
| FBD08_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte7, Bit0-2 |
| FBD08_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte7, Bit7 |
| FBD09_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte8, Bit0-2 |
| FBD09_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte8, Bit7 |
| FBD10_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte9, Bit0-2 |
| FBD10_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte9, Bit7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-ubat"></a>
### STATUS_HS_UBAT

aktueller Status "UBat" aller HSs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5D Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HS01_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte0, Bit0-2 |
| HS01_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte0, Bit7 |
| HS02_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 Byte1, Bit0-2 |
| HS02_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte1, Bit7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fbd-feldstaerke"></a>
### STATUS_FBD_FELDSTAERKE

aktueller Status "Feldstaerke" der FBDs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5E Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBD_QUELLE | unsigned char | Bereich 0-255 Byte0 |
| FBD_KEYID_PRSL | unsigned char | Bereich 0-255 Byte1 |
| FBD_KEYID_DIAG | unsigned char | Bereich 0-255 Byte2 |
| FBD_QUANT | unsigned char | Bereich 0-255 Byte3 |
| FBD_QUANT_MIN | unsigned char | Bereich 0-255 Byte4 |
| FBD_QUANT_MAX | unsigned char | Bereich 0-255 Byte5 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wup"></a>
### STATUS_WUP

aktueller Status "Wake-Up-Pattern" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $5F Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| WUP | binary | Byte0-2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fbd-personalisierung"></a>
### STATUS_FBD_PERSONALISIERUNG

aktueller Status "Personalisierung" der FBDs KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $60 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBD0_PERSON | unsigned char | Bereich 0-255 Byte0 |
| FBD1_PERSON | unsigned char | Bereich 0-255 Byte1 |
| FBD2_PERSON | unsigned char | Bereich 0-255 Byte2 |
| FBD3_PERSON | unsigned char | Bereich 0-255 Byte3 |
| FBD4_PERSON | unsigned char | Bereich 0-255 Byte4 |
| FBD5_PERSON | unsigned char | Bereich 0-255 Byte5 |
| FBD6_PERSON | unsigned char | Bereich 0-255 Byte6 |
| FBD7_PERSON | unsigned char | Bereich 0-255 Byte7 |
| FBD8_PERSON | unsigned char | Bereich 0-255 Byte8 |
| FBD9_PERSON | unsigned char | Bereich 0-255 Byte9 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fertig-transp-werkst"></a>
### STATUS_FERTIG_TRANSP_WERKST

1 Byte lesen: "Fertigung/Transport/Werkstatt-MODE" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$100A Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FE_TR_WE_STATUS | unsigned char | "Fe_Tr_We-Mode": ======&gt; Byte0 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vehicle-production-date"></a>
### STATUS_VEHICLE_PRODUCTION_DATE

8 ASCII Byte Production Date KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1009 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATE | string | ausgelesene Production Date |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-repeat-table"></a>
### STATUS_REPEAT_TABLE

8 Byte Repeat Table Version KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x100D Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VERSION | binary | ausgelesene Version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

17 ASCII Byte Fahrgestell-Nummer KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0x1010 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FGNUMMER | string | ausgelesene Fahrgestellnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ho-code"></a>
### STATUS_HO_CODE

8 Byte "HO-Codierung" lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1013 Modus  :  Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DEALER_ORG | string | "HO-Codierung": Byte0-4 |
| FIRST_REG_TIME_DAY | unsigned char | "Tag" Byte5 |
| FIRST_REG_TIME_MONTH | unsigned char | "Monat" Byte6 |
| FIRST_REG_TIME_YEAR_2_DIGITS | unsigned char | "Jahr" Byte7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fzg-zustand"></a>
### STATUS_FZG_ZUSTAND

14 Byte "Fahrzeug-Zustand" lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1015 Modus  :  Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MILE_KM | binary | "Meilen/Km": 0-16.xxx.xxx Byte0-2 |
| DISP_HOURS | unsigned char | "Stunden":  0-23 Byte4 |
| DISP_MINUTES | unsigned char | "Minuten":  0-59 Byte5 |
| DISP_DATE_DAY | unsigned char | "Tag":   1-31 Byte5 |
| DISP_DATE_MONTH | unsigned char | "Monat": 1-12 Byte6 |
| DISP_DATE_YEAR | unsigned int | "Jahr":  1-65535 Byte7-8 |
| FLUIDLEVEL_TANK | unsigned char | "FLLV_FUTA":  0-254 l Byte11 |
| BATTERY_VOLTAGE | real | "UBat":  0-4094 * 15mV = 61410mV Byte9-10-Bit3(12Bit) |
| ENGINE_TEMPERATURE | int | "TEMP_ENG":  0-254 =&gt; -48...+206 Grad Celsius Byte12 |
| KLEMMENSTATUS | unsigned char | Bit0-1 "Klemme__R":  00=OFF/01=ON/1?=ungueltig Bit2-3 "Klemme_15":  00=OFF/01=ON/1?=ungueltig Bit4-5 "Klemme_50":  00=OFF/01=ON/1?=ungueltig Bit6-7 "Schl_Valid": 00=OFF/01=ON/1?=ungueltig Byte13 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fzg-typ"></a>
### STATUS_FZG_TYP

11 Byte "Fahrzeug-Type" lesen KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1011 Modus  :  Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR_ART | unsigned char | 4=benzin_direkt N73B60, N73B68, N43B20 5=benzin_normal M54B30, N62B36, N62B44, M54B22, M54B24, M54B25, S85B50 6=diesel_direkt M57D30, M67D40, M47D20, M57D25 7=diesel_normal Byte0 / Bits 3-0 |
| TYP_LENKUNG | unsigned char | 1=linkslenker, alle Linkslenker 2=rechtslenker, alle Rechtslenkercomment Byte0 / Bits 7-4 |
| ZYLINDER_ZAHL | unsigned char | 4=4 zylinder, alle mit Motor M4x, N4x 6=6 zylinder, alle mit Motor M5x, N5x 8=8 zylinder, alle mit Motor M6x, N6x 10=10 zylinder, alle mit Motor S85B50 (M5) 12=12 zylinder, alle mit Motor M7x, N7x Byte1 / Bits 3-0 |
| GETRIEBE_GAENGE | unsigned char | 5=5 gaenge, E6x ohne SA205 \|\| E6x + SA205 + (N43B20 \|\| M47D20) 6=6 gaenge, alle anderen SA205 und SA206 Sequentielles-M-Getriebe (E6x, E65, E66, E67) Byte1 / Bits 7-4 |
| BAUART | unsigned char | 1=limousine, E65,E66, E60 alle Varianten 2=coupe, E61 3=touring, E63 4=cabrio, E64 5=roadster, noch nicht 6=compact, noch nicht 7=sicherheitsfahrzeug, E67 Byte2 |
| BAUREIHE | unsigned char | 1=e65 2=e66 3=e67 4=e60 5=e61 6=e63 7=e64 8=e81,e87,e90 9=rr1 Byte3 |
| MOTOR_HUBRAUM | unsigned char | 0x14=n43b20, m47d20 0x19=m57d25 0x1E=m57d30, m54b30 0x16=m54b22 0x18=m54b24 0x19=m54b25 0x24=n62b36 0x2C=n62b44 0x27=m67d40 0x3C=n73b60 0x44=n73b68 0x32=s85b50 Byte4 |
| LAENDERVARIANTE_BNDB | unsigned char | 1=ece, alle ohne nachfolgende Zeilen 2=us, US ohne Kanada 3=deutschland, LA 801 Deutschland 4=gb, LA 812 Gross Britaninen 5=japan, LA 807 Japan 6=australien, LA 810 Australien 7=korea, LA 802 Korea 8=brasilien, LA xxx Brasilien   --&gt; keine LA, kann nicht gesteuert werden 9=aegypten, 821 Aegypten 10=golf, LA 822 Golfstaaten 11=suedafrika, LA 824 Suedafrika 12=kanada, LA 838 Kanada 13=taiwan, LA 846 Taiwan (National-China) 14=indien, LA xxx Indien      --&gt; keine LA, kann nicht gesteuert werden 15=malaysia, LA xxx Malaysia    --&gt; keine LA, kann nicht gesteuert werden 16=thailand, LA xxx Thailand    --&gt; keine LA, kann nicht gesteuert werden 17=indonesien, LA xxx Indonesien  --&gt; keine LA, kann nicht gesteuert werden 18=philippinen, LA xxx Philippinen --&gt; keine LA, kann nicht gesteuert werden 19=vietnam, LA xxx Vietnam     --&gt; keine LA, kann nicht gesteuert werden 20=mexiko, LA xxx Mexiko      --&gt; keine LA, kann nicht gesteuert werden 21=belgien, LA xxx Belgien     --&gt; keine LA, kann nicht gesteuert werden Byte5 |
| GETRIEBE_TYP | unsigned char | 0=handschaltung, alle ausser naechste Zeilen 1=automatik, RR01 (in Klaerung mit H. Fuerst) 2=schrittschaltung, alle E65, SA205 3=ssg_schaltung, SA206, fuer Getriebevariante SSG Byte6, Bits 3-0 |
| CLASS_PWR | unsigned char | 0=alle sonstigen Varianten 1=klasse_1, N52B30_OL, M54B30_OL, M57D30_OL, N46B20_OL 2=klasse_2, schrittschaltung, alle E65, SA205 Byte6, Bits 5-4 |
| KLASSE_BATTERIE | unsigned char | Codierung Batterieklasse : Batteriegroesse, Technologie 1=  80Ah Ca/Ca 2=  90Ah Ca/Ca 3=  110Ah Ca/Ca 0=  alle PL2 Varianten (bis Funktion durch Hr. Boehm abgestimmt) Byte7 |
| STROM_RUHE | unsigned char | 4=alle 4*20mA Byte8 |
| STROM_KS_MIN | unsigned char | 80=alle 800A Byte9 |
| STROM_KS_MAX | unsigned char | 100=alle 1000A Byte10 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bos-cc-daten"></a>
### STATUS_BOS_CC_DATEN

Lesen von 32 Byte "BOS_CC-Daten" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1016-1018 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_CC_INDEX | int | Werte: 1...3 ===&gt;Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RAM_BOS_ARRAY | binary | Byte0-31 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fsd-daten"></a>
### STATUS_FSD_DATEN

Lesen von 32 Byte "FSD-Daten" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1019-101A Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FSD_INDEX | int | Werte: 1...2 ===&gt;Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RAM_FSD_ARRAY | binary | Byte0-31 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeugauftrag"></a>
### STATUS_FAHRZEUGAUFTRAG

Liest 16 Byte "Fahrzeugauftrag" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=3F00...3F13 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NUMMER | int | Werte: 0...19 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_DATA | binary | Flash Data |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-diagnose"></a>
### STEUERN_CAS_DIAGNOSE

Schreibt 6 Byte "Digital Outputs" KWP2000: $30 InputOutputControlByLocalIdentifier LocalIdentifier=$02 $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EWS_TOGGELN | unsigned char | Bereich 0/1 ======&gt; Byte0, Bit0 |
| TXD_TOGGELN | unsigned char | Bereich 0/1 ======&gt; Byte0, Bit1 |
| IN_ZAS_BLSDISC | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit0 |
| IN_EGS_PNDISC | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit1 |
| IN_VR_DISC | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit2 |
| IN_ER_DISC | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit3 |
| HKIT | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit4 |
| IN_MHK_ZUDISC | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit5 |
| IN_HTLSTLG_EINDISC | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit6 |
| IN_FB_MOTFERNSTARTDISC | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit7 |
| IN_RESERVE_1_DISC | unsigned char | Bereich 0/1 ======&gt; Byte2, Bit0 |
| FBD_DIAG_FKT | unsigned char | Bereich 0-255 ======&gt; Byte3 |
| FBD_DIAG_PRSLNR | unsigned char | Bereich 0-255 ======&gt; Byte4 |
| RF_FELDSPULE_EIN | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit0 |
| SCI_TELEGRAMM_CLR | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit1 |
| SET_KL30X_ON | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit2 |
| SET_KL30X_OFF | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit3 |
| SET_KL30G_ON | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit4 |
| SET_KL30G_OFF | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit5 |
| SET_KLR_ON | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit6 |
| SET_KLR_OFF | unsigned char | Bereich 0/1 ======&gt; Byte5, Bit7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-isn"></a>
### STEUERN_ISN

Schreibt  4Byte "ISN" und kopiert diesen auf beide  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $01 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ISN_CODE | string | "ISN": z.B. "0x00,0x00,0x55,0xAA" ======&gt; Byte0-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mech-schluesselcode"></a>
### STEUERN_MECH_SCHLUESSELCODE

Schreibt 10 Byte "mechan. Schluessel-Code"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $02 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "HA00012345" ======&gt; Byte0-9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-frequenz"></a>
### STEUERN_SCHLUESSEL_FREQUENZ

Schreibt 1 Byte "Schluessel-Frequenz"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $03 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEQ_FREQ | unsigned char | "Freq": 0-255 ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-prog-location-datum"></a>
### STEUERN_PROG_LOCATION_DATUM

Schreibt 3 Byte "Programmier-Ort/Datum"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $04 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROG_LOCATION | unsigned char | "Ort":   0-15 ======&gt; Byte0, Bit4-7 |
| PROG_TIME_DAY | unsigned char | "Tag":   1-31 ======&gt; Byte1 |
| PROG_TIME_MONTH | unsigned char | "Monat": 1-12 ======&gt; Byte0, Bit0-3 |
| PROG_TIME_YEAR_2_DIGITS | unsigned int | "Jahr":  0-99 ======&gt; Byte2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zv-authentisierung"></a>
### STEUERN_ZV_AUTHENTISIERUNG

Schreibt 4 Byte "ZV-Authentisierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $05 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "0x11,0x22,0x33,0x44" ======&gt; Byte0-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elv-authentisierung"></a>
### STEUERN_ELV_AUTHENTISIERUNG

Schreibt 4 Byte "ELV-Authentisierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $05 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "0x11,0x22,0x33,0x44" ======&gt; Byte0-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-transponderkennung"></a>
### STEUERN_TRANSPONDERKENNUNG

Schreibt 3 Byte "Transponder-Aktivierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $06 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "0xAA,0xAA,0xAA" ======&gt; Byte0-2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-trsp-fahrzykluszaehler"></a>
### STEUERN_TRSP_FAHRZYKLUSZAEHLER

Schreibt 4 Byte "Transponder-Fahrzykluszaehler"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $07 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZAEHLER_HIGH_WORD | unsigned int | ======&gt; Byte0-1 |
| ZAEHLER_LOW_WORD | unsigned int | ======&gt; Byte2-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-init-kennung"></a>
### STEUERN_CAS_INIT_KENNUNG

Schreibt 3 Byte "Initialisierungs-Kennung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $08 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "0xAA,0xAA,0xAA" ======&gt; Byte0-2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bdm-sperren"></a>
### STEUERN_BDM_SPERREN

BDM Sperren (only in special mode with BDM interface!!!)  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $09 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4-sk"></a>
### STEUERN_EWS4_SK

17 "EWS4-data" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$C001 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Byte0 MODE-strings vgl.: table STEUERN_EWS4_MODE TEXT |
| DATA | string | Byte1...16 16 Byte Daten (SecretKey), falls MODE = WRITE_SERVER_SK/WRITE_CLIENT_SK KEINE Daten nötig, falls MODE = LOCK_SERVER_SK/LOCK_CLIENT_SK |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4-key"></a>
### STEUERN_EWS4_KEY

Schreibt 64 Byte EWS key  KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$C000 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "0x11,0x22,0x33,0x44..." ======&gt; Byte0-63 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dme-ringbuffer"></a>
### STEUERN_DME_RINGBUFFER

Schreibt 31 Byte "DME-Ringpuffer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0A Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "1,2,03,0x04,0x05,...." ======&gt; Byte0-30 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zvfh-ringbuffer"></a>
### STEUERN_ZVFH_RINGBUFFER

Schreibt 64+1 Byte "ZV/FH-Ringpuffer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0B Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BUFFER_POINTER | unsigned char | ======&gt; Byte 0 |
| DATEN | string | "Daten": z.B. "1,2,03,0x04,0x05" ======&gt; Byte 1-64 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ict-byte"></a>
### STEUERN_ICT_BYTE

Internal Circuit Byte Schreiben  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0E Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ICT_BYTE | unsigned char | ======&gt; Byte 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluesseldaten"></a>
### STEUERN_SCHLUESSELDATEN

Schreibt 17 Byte "Schluessel-Daten"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $10...$19 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NUMBER | int | "Schl-Nr": 1-10 ======&gt; Array-Index |
| STATUS_BYTE1 | unsigned char | "Status1": 0-255 ======&gt; Byte 0 |
| STATUS_BYTE2 | unsigned char | "Status1": 0-255 ======&gt; Byte 1 |
| INITIALISIERUNGSSTATUS | unsigned char | "Init-Status": 0-255 ======&gt; Byte 2 |
| IDENTIFIER | string | "Identifier": (z.B. 0x01,0x02,0x03,0x04) ======&gt; Byte 3-6 |
| SECRET_KEY | string | "Secret Key": (z.B. 0x01,0x02,0x03,0x04,0x05,0x06) ======&gt; Byte 7-12 |
| CONFIG_BYTE | unsigned char | Config-Byte ======&gt; Byte 13 |
| PASSWORD_TRANSPONDER | string | "Password-Transponder": (z.B. 0x01,0x02,0x03) ======&gt; Byte 14-16 |
| CRC_BYTE | unsigned char | "CyclicRedundancyCheck": 0-255 ======&gt; Byte 17 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-gesperrt"></a>
### STEUERN_SCHLUESSEL_GESPERRT

Schreibt 1 Byte "Schluessel-Sperre"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $20 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NUMBER | unsigned int | Schluesselnummer: 1...10 ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-freigeben"></a>
### STEUERN_SCHLUESSEL_FREIGEBEN

Schreibt 1 Byte "Schluessel-Nummer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $21 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NUMBER | unsigned int | "Nr.":   1-10 ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aktualisieren-chip-card-daten"></a>
### AKTUALISIEREN_CHIP_CARD_DATEN

Schreibt 1 Byte  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $23 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CHIP_CARD_DATA | unsigned char | Bereich: 0-255 ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-basestation"></a>
### STEUERN_BASESTATION

Schreibt 5 Byte "Basestation-Vorgabewerte"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $26 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAGE0 | unsigned char | "Page0": 0-15 ======&gt; Byte0 |
| PAGE1 | unsigned char | "Page1": 0-15 ======&gt; Byte1 |
| PAGE2 | unsigned char | "Page2": 0-15 ======&gt; Byte2 |
| PAGE3 | unsigned char | "Page3": 0-15 ======&gt; Byte3 |
| SAMPLING_TIME | unsigned char | "STime": 0-63 ======&gt; Byte4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kommunikation-parameter"></a>
### STEUERN_KOMMUNIKATION_PARAMETER

Schreibt 1 Byte "Kommunikation Parameter"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $28 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAGNOSE_SETZT_FORT | unsigned char | Bereich 0/1 ======&gt; Byte0,Bit0 |
| CRYPTO_PASSWORD | unsigned char | Bereich 0/1 ======&gt; Byte0,Bit1 |
| AUTHENT_DIAGN_CAS | unsigned char | Bereich 0/1 ======&gt; Byte0,Bit2 |
| ABZUGSSPERRE_ON_OFF | unsigned char | Bereich 0/1 ======&gt; Byte0,Bit3 |
| RF_FELD_OHNE_SCHLUESSSEL_EIN | unsigned char | Bereich 0/1 ======&gt; Byte0,Bit4 |
| S_DIAG_STARTINIT | unsigned char | Bereich 0/1 ======&gt; Byte0,Bit5 |
| S_DIAG_DIS_CYA | unsigned char | Bereich 0/1 ======&gt; Byte0,Bit6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cmd-read-page-trsp"></a>
### STEUERN_CMD_READ_PAGE_TRSP

Schreibt 1 Byte "Transponder Page"  KWP 2000: $3B WriteDataByLocalIdentifier LocalIdentifier $29 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAGE_NUMMER | unsigned char | "Page": 0-7,0xFF,"WUP": 0xFE Diagnosed, 4 Pages: 0xFD ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-adr-xtrsp"></a>
### STEUERN_ADR_XTRSP

Schreibt 4 Byte "XTRSP-Adresse"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $2B Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_HIGH | unsigned int | "High": 0-65535 ======&gt; Byte0-1 |
| ADRESSE_LOW | unsigned int | "Low":  0-65535 ======&gt; Byte2-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-page-trsp"></a>
### STEUERN_PAGE_TRSP

Schreibt 5 Byte "TRSP-Page"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $2C Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAGE | unsigned char | "Page": 0-7, 0xFF, "WUP": 0xFE ======&gt; Byte0 |
| DATA_HIGH | unsigned int | "High": 0-65535 ======&gt; Byte1-2 |
| DATA_LOW | unsigned int | "Low":  0-65535 ======&gt; Byte3-4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sequence-counter-xtrsp"></a>
### STEUERN_SEQUENCE_COUNTER_XTRSP

Schreibt 4 Byte "XTRSP, Sequ.-Counter"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $2E Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA_HIGH | unsigned int | "High": 0-65535 ======&gt; Byte0-1 |
| DATA_LOW | unsigned int | "Low":  0-65535 ======&gt; Byte2-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fbd-daten"></a>
### STEUERN_FBD_DATEN

Schreibt 15 Byte "Daten fuer eine FBD" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $50-$59 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_NUMMER | int | Werte: 1...10 ======&gt; LID |
| KEY_NUMBER_WORD | string | Schluessel-Nr ======&gt; Byte0-1 |
| SECRET_KEY_HIGH | string | "SECRET_KEY_HIGH": z.B. "1,2" ======&gt; Byte2-3 |
| SECRET_KEY_LOW | string | "SECRET_KEY_HIGH": z.B. "1,2,3,4" ======&gt; Byte4-7 |
| RANDOM_FBD | string | "SECRET_KEY_HIGH": z.B. "1,2,3,4" ======&gt; Byte8-11 |
| LAUF_NR | unsigned char | Personalisierung Nummer ======&gt; Byte12 |
| UBAT_STAT | unsigned char | Hex-Antwort von SG ======&gt; Byte13, Bit0-7 |
| STAT_FBD | unsigned char | Bereich ======&gt; Byte14, Bit0-7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fbd-ubat"></a>
### STEUERN_FBD_UBAT

Schreibt 10 Byte "UBAT fuer alle FBD" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5C Modus:   Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FBD01_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte0, Bit0-2 |
| FBD01_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte0, Bit7 |
| FBD02_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte1, Bit0-2 |
| FBD02_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit7 |
| FBD03_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte2, Bit0-2 |
| FBD03_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte2, Bit7 |
| FBD04_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte3, Bit0-2 |
| FBD04_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte3, Bit7 |
| FBD05_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte4, Bit0-2 |
| FBD05_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte4, Bit7 |
| FBD06_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte5, Bit0-2 |
| FBD06_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 Byte5, Bit7 |
| FBD07_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte6, Bit0-2 |
| FBD07_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte6, Bit7 |
| FBD08_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte7, Bit0-2 |
| FBD08_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte7, Bit7 |
| FBD09_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte8, Bit0-2 |
| FBD09_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte8, Bit7 |
| FBD10_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte9, Bit0-2 |
| FBD10_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte9, Bit7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hs-ubat"></a>
### STEUERN_HS_UBAT

Schreibt 2 Byte "UBAT fuer alle HS" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5D Modus:   Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HS01_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte0, Bit0-2 |
| HS01_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte0, Bit7 |
| HS02_UBAT_STAT_CNTR | unsigned char | Bereich 0-7 ======&gt; Byte1, Bit0-2 |
| HS02_UBAT_STAT_FLAG | unsigned char | Bereich 0/1 ======&gt; Byte1, Bit7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fbd-feldstaerke"></a>
### STEUERN_FBD_FELDSTAERKE

Schreibt 6 Byte "FBD-Feldstaerke" KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5E Modus:   Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FBD_QUELLE | unsigned char | Bereich 0-255 ======&gt; Byte0 |
| FBD_KEYID_PRSL | unsigned char | Bereich 0-255 ======&gt; Byte1 |
| FBD_KEYID_DIAG | unsigned char | Bereich 0-255 ======&gt; Byte2 |
| FBD_QUANT | unsigned char | Bereich 0-255 ======&gt; Byte3 |
| FBD_QUANT_MIN | unsigned char | Bereich 0-255 ======&gt; Byte4 |
| FBD_QUANT_MAX | unsigned char | Bereich 0-255 ======&gt; Byte5 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wup"></a>
### STEUERN_WUP

Schreibt 3 Byte "Wake-Up-Pattern"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $5F Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WUP_BYTE_HIGH | unsigned char | "High": 0-255 ======&gt; Byte0 |
| WUP_BYTE_MIDDLE | unsigned char | "Mid":  0-255 ======&gt; Byte1 |
| WUP_BYTE_LOW | unsigned char | "Low":  0-255 ======&gt; Byte2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fbd-personalisierung"></a>
### STEUERN_FBD_PERSONALISIERUNG

Schreibt 10 Byte "FBD Personalisierung Daten"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $60 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FBD0_PERSON | unsigned char | "High": 0-255 ======&gt; Byte0 |
| FBD1_PERSON | unsigned char | "High": 0-255 ======&gt; Byte1 |
| FBD2_PERSON | unsigned char | "High": 0-255 ======&gt; Byte2 |
| FBD3_PERSON | unsigned char | "High": 0-255 ======&gt; Byte3 |
| FBD4_PERSON | unsigned char | "High": 0-255 ======&gt; Byte4 |
| FBD5_PERSON | unsigned char | "High": 0-255 ======&gt; Byte5 |
| FBD6_PERSON | unsigned char | "High": 0-255 ======&gt; Byte6 |
| FBD7_PERSON | unsigned char | "High": 0-255 ======&gt; Byte7 |
| FBD8_PERSON | unsigned char | "High": 0-255 ======&gt; Byte8 |
| FBD9_PERSON | unsigned char | "High": 0-255 ======&gt; Byte9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vehicle-production-date"></a>
### STEUERN_VEHICLE_PRODUCTION_DATE

8 ASCII "Vehicle Production Date" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1009 Full Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATE | string | "Date" 8 x ASCII (0-9) ======&gt; Byte0-7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrgestellnummer"></a>
### STEUERN_FAHRGESTELLNUMMER

17 ASCII "Fahrgestellnummer" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1010 Full Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NUMMER | string | "Fahrgestellnummer" 17 x {1...0A...Z} ======&gt; Byte0-16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ho-code"></a>
### STEUERN_HO_CODE

8 Byte "HO-Codierung" schreiben KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=$1013 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEALER_ORG | string | "HO-Codierung" ======&gt; Byte0-4 |
| FIRST_REG_TIME_DAY | unsigned char | "Tag" ======&gt; Byte5 |
| FIRST_REG_TIME_MONTH | unsigned char | "Monat" ======&gt; Byte6 |
| FIRST_REG_TIME_YEAR_2_DIGITS | unsigned char | "Jahr" ======&gt; Byte7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrzeugauftrag"></a>
### STEUERN_FAHRZEUGAUFTRAG

Schreibt 16 Byte "Fahrzeugauftrag" KWP2000: $2E WriteDataByCommonIdentifier CommonIdentifier=3F00...3F13 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NUMMER | int | Werte: 0...19 ======&gt; CID |
| BLOCK_DATA | string | "Block Data": z.B. 0x01,0x02,0x03,0x04,0x05,0x06... ======&gt; Byte 0-15 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-schreiben"></a>
### C_FA_SCHREIBEN

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-fertig-transp-werkst"></a>
### SET_FERTIG_TRANSP_WERKST

Initialisiert den Fertigung/Transport/Werkstatt-MODE KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $0C Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | unsigned char | Werte: 0-255 ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dme-startwert-abgleich"></a>
### DME_STARTWERT_ABGLEICH

Kopiert die ISN auf beide Wechselcodes KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $20 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-key-mode"></a>
### SET_KEY_MODE

1 Byte =&gt; Command 0/1/2/3/-/5/6/7 11 Byte =&gt; Command -/-/-/-/4/-/-/- Startet einen KEY_MODE Befehl KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $21 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COMMAND | string | "Befehl": 0-7 table Key_Mode_Befehle NAME TEXT ======&gt; Byte0 |
| DATEN | string | "Daten": Nur fuer START_AUTH_DIAG(=4) ======&gt; Byte1-16 (z.B. 0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-key-init"></a>
### SET_KEY_INIT

Initialisiert den KEY-MODE KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $22 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| NR_OF_NOT_INIT_KEYS | unsigned char | 0 =    all 10 KEYs are correct 1 = 1 or more KEYs not correct |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-signaturpruefung"></a>
### SIGNATURPRUEFUNG

Aktiviert die Signaturpruefung des Flash-ROM KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $23 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SIGNATUR_ERGEBNIS | unsigned char | 0 = incorrect 1 = correct |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-auftrag-cas"></a>
### C_C_AUFTRAG_CAS

Codierd schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskend) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Byted (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortd (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierd Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-c-lesen-cas"></a>
### C_C_LESEN_CAS

Codierd lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskend) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Byted (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortd (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierd Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierd |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-schreiben-cas"></a>
### C_C_SCHREIBEN_CAS

Codierd schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskend) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Byted (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortd (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierd Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-istufe-lesen-cas"></a>
### ISTUFE_LESEN_CAS

I_Stufe lesen KWP2000: $22   ReadDataByCommonIdentifier $100B Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ISTUFE | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-istufe-schreiben-cas"></a>
### ISTUFE_SCHREIBEN_CAS

I_Stufe schreiben KWP2000: $2E   WriteDataByCommonIdentifier $100B Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ISTUFE | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cbs-version"></a>
### STATUS_CBS_VERSION

I_Stufe lesen KWP2000: $22   ReadDataByCommonIdentifier $1014 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CBS_VERSION | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cbs-version"></a>
### STEUERN_CBS_VERSION

I_Stufe schreiben KWP2000: $2E   WriteDataByCommonIdentifier $1014 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_VARIANT | unsigned int | "Vaues": 0-65535 ======&gt; Byte0-1 |
| CBS_VERSION | unsigned char | "Values":  0-255 ======&gt; Byte2 |
| CC_CONSISTENCE | unsigned char | "Values": 0xAA ======&gt; Byte3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sdiag"></a>
### SDIAG

Universaler Diagnosebefehl Speziell fuer Tools SDIAG vom SIEMENS VDO Regensburg entwickelt KWP2000: $XX Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Der Binaerbuffer hat folgenden Aufbau Byte 0              : SID Byte 1              : Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RESULT_DATEN | binary | Result |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cc-daten-arg"></a>
### STATUS_CC_DATEN_ARG

Lesen von 32 Byte "CC-Daten" KWP 2000: $31 StartRoutineByLocaldentifier $25 READ_CC_DATEN_ARG Local=0x00 - 0x19 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NR_CC_DATEN | int | Werte: 0x00...0x19 ===&gt;Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CC_ARRAY | binary | Byte0-31 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-elv-ident"></a>
### ELV_IDENT

KWP 2000: $21 ReadDataByLocaldentifier Local=$05 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ELV_SERIEN_NUMMER | binary | ===&gt;Byte5-10 |
| ELV_HW_STAND | int | Byte1-2 |
| ELV_SW_STAND | int | Byte3-4 |
| ELV_SERIEN_NUMMER_DECODE | string | Byte5-10 |
| ELV_HW_STAND_DECODE | string | Byte1-2 |
| ELV_SW_STAND_DECODE | string | Byte3-4 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fndcom"></a>
### STATUS_FNDCOM

3 Byte des EEPROM FNDCOM_Id Block KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $61 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FNDCOM_ID | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fndcom"></a>
### STEUERN_FNDCOM

Schreibt  3Byte im EEPROM-Block FNDCOM_Id  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $61 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FNDCOM_ID | string | FNDCOM_ID: z.B. "0x00,0x00,0x55,0xAA" ======&gt; Byte0-2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-authent-fndcom"></a>
### STATUS_AUTHENT_FNDCOM

1 Byte des Authentisierung des FNDCOM KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $62 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUTHEN_FNDCOM | int | 0 - nicht Authentisiert 1 - Authentisiert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fndcom-anlernen"></a>
### STEUERN_FNDCOM_ANLERNEN

KWP2000: $31 StartRoutineByLID LocalIdentifier $26 00 XX Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FNDCOM_ZEIT | int | Fenster Zeit 0 bis 255 Sekunden" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FNDCOM_ID | string | ID von FNDCOM" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fndcom-funktion"></a>
### STATUS_FNDCOM_FUNKTION

KWP2000: $31 StartRoutineByLID LocalIdentifier $26 00 XX Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FNDCOM_ZEIT | int | Fenster Zeit 0 bis 255 Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FNDCOM_KNOPF | int | Knopf Nummer |
| FNDCOM_KNOPF_INTENSITY | int | Knopf Intensity |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rdu"></a>
### STATUS_RDU

Infospeicher lesen (alle Info-Meldungen) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory Infospeicher lesen detail (hier 0x9810) KWP2000: $22 ReadDataByCommonIdentifier $20XX dtcShadowMemoryEntry, wobei XX = Ort des RDU-INFO-Eintrags Liest Datum/Urzeit zum INFO_Eintrags 0x9810 KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $27

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RDU_INFO_AVAILABLE | int | 0 Keine Informationen über den RDU vorhanden (z.B. noch nie ausgeführt, RDU-INFO existiert nicht) 1 Informationen zu einem RDU vorhanden |
| STAT_RDU_NR | int | Fehlersymptom als Zahl 0 - "Not Available", falls STAT_RDU_INFO_AVAILABLE gleich 0 |
| STAT_RDU_TXT | string | Fehlersymptom als Text Werte aus Tabelle RDU_NUMBER 0 - "Not Available", falls STAT_RDU_INFO_AVAILABLE gleich 0 |
| STAT_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km 0, falls STAT_RDU_INFO_AVAILABLE gleich 0 |
| STAT_DATE_TIME | string | Datum des INFO-Eintrags Format: "MM/DD/JJJJ, HH:MM 24h" "--/--/----, --:-- 24h", falls ungültiges Datum/Zeit auf dem CAN, oder falls STAT_RDU_INFO_AVAILABLE gleich 0 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-elv-werte"></a>
### STATUS_ELV_WERTE

KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $7A Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ELV_KL30L | real | Byte0-1 |
| STAT_ELV_KL30E | real | Byte2-3 |
| STAT_ELV_RESET_URSACHE | string | Byte4 |
| STAT_ELV_SPEED | string | Byte5 |
| STAT_ELV_SPEED_ZEIGER | string | Byte5 |
| STAT_ELV_KL15EINDISC | int | Byte6, Bit 0 |
| STAT_ELV_WD_ENDISC | int | Byte6, Bit 1 |
| STAT_IN_KL3KMH_DISC | int | Byte6, Bit 2 |
| STAT_IN_ELVHW_DIAGDISC | int | Byte6, Bit 3 |
| STAT_ELV_MSG_BA | int | Byte6, Bit 4 |
| STAT_ELV_MSG_15 | int | Byte6, Bit 5 |
| STAT_IN_KL3KMH_DELAYDISC | int | Byte6, Bit 6 |
| STAT_ELV_SELBSTHEIL_AKTIV | int | Byte6, Bit 7 |
| STAT_ELV_ACTUEL_STATE | string | table ELV_STATE NAME Byte7 |
| STAT_ELV | string | ENTRIEGELT oder VERRIEGELT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elvcounter-cas-loeschen"></a>
### STEUERN_ELVCOUNTER_CAS_LOESCHEN

Loeschen EscapeCounter von CAS KWP 2000: $21 $3B ReadWriteDataByLocalIdentifier LocalIdentifier $79 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ESCAPE_URSACHEN | string | Ursachen, die escape inkrementiert haben |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elvcounter-elv-loeschen"></a>
### STEUERN_ELVCOUNTER_ELV_LOESCHEN

Loeschen EscapeCounter von ELV KWP 2000: $21 $3B ReadWriteDataByLocalIdentifier LocalIdentifier $79 Modus   : Default

_No arguments._

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
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (129 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (90 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [KEY_MODE_BEFEHLE](#table-key-mode-befehle) (8 × 3)
- [ELV_STATE](#table-elv-state) (26 × 2)
- [EWS4_KEY_STATE](#table-ews4-key-state) (18 × 3)
- [STEUERN_EWS4_MODE](#table-steuern-ews4-mode) (3 × 4)
- [RDU_NUMBER](#table-rdu-number) (5 × 2)

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

Dimensions: 129 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xD904 | K_CAN_Leitungsfehler |
| 0xD905 | K_CAN_HIGH |
| 0xD906 | GroundShift |
| 0xD907 | Bus_Off |
| 0xD90C | CAN_ENG_FEHLER |
| 0xD90D | CAN_FEHLER_2LEITUNGEN |
| 0xD93C | Fehlerwert_erhalten |
| 0xD93D | Unplausibles_Signal |
| 0xD93E | Telegramm_Timeout_beim_Emfang |
| 0xD93F | Fehler_beim_Emfang_NM_Botschaft |
| 0xD940 | Fehlerwert_gesendet |
| 0xD941 | Unplausibles_Signal1 |
| 0xD942 | Telegramm_Timeout_beim_Senden |
| 0xE904 | K_CAN_LOW_PER |
| 0xE905 | K_CAN_HIGH_PER |
| 0xE906 | GroundShift_PER |
| 0xE93C | Fehlerwert_erhalten_PER |
| 0xE93D | Unplausibles_Signal_PER |
| 0xE93E | Telegramm_Timeout_beim_Emfang_PER |
| 0xE93F | Fehler_beim_Emfang_NM_Botschaft_PER |
| 0xE940 | Fehlerwert_gesendet_PER |
| 0xE941 | Unplausibles_Signal1_PER |
| 0xE942 | Telegramm_Timeout_beim_Senden_PER |
| 0xE943 | Fehler_beim_Senden_NM_Botschaft_PER |
| 0xA0A8 | BSW_RAM_CRC_FEHLER |
| 0xA0A9 | BSW_SYSTEM_FEHLER |
| 0xA0AA | BSW_REGISTER_FEHLER |
| 0xA0AB | BSW_ProgFlash_CRC_FEHLER |
| 0xA0AC | BSW_SG_FEHLER_COP_CM_TRAP |
| 0xA0AD | EEPROM_Schreibe_Fehler |
| 0xA0AE | Energiesparmode_aktiv |
| 0xA0AF | FEHLER_EXTERNAL_WATCHDOG |
| 0xA0B0 | SG_Eingang_Bremslicht |
| 0xA0B1 | SG_Eingang_P_N |
| 0xA0B2 | Fehler_CAS_Versorgung |
| 0xA0B3 | Fehler_Ansteurung_Anlasser_KL50 |
| 0xA0B4 | Fehler_Motorstart_Anlasserbetrieb |
| 0xA0B5 | Signalerkennung_Geschwindigkeit_Fehler |
| 0xA0B6 | Interlock_PLOCK_Fehler |
| 0xA0B8 | Hallsensor_RAST_KS |
| 0xA0B9 | Hallsensor_EJECT_KS |
| 0xA0BA | Hallsensor_SSTA_KS |
| 0xA0BB | Hallsensor_SSTB_KS |
| 0xA0BC | Hubmagnet_AZSP |
| 0xA0BD | Treiber_KL15_WUP_KS |
| 0xA0BE | Treiber_KL15_1_FZG_KS |
| 0xA0BF | Treiber_KL15_2_FZG_KS |
| 0xA0C0 | Treiber_KL15_3_FZG_KS |
| 0xA0C1 | Treiber_KL50L_KS |
| 0xA0C2 | Treiber_KL50RS_KS |
| 0xA0C3 | Treiber_KL15_WUP_RS_KS |
| 0xA0C4 | Treiber_KL15_4_FZG_KS |
| 0xA0C5 | MFS_Signal_fehlt |
| 0xA0C6 | Treiber_KLR_KS |
| 0xA0C7 | Treiber_KLR_MRS_KS |
| 0xA0C8 | Komfort_Schliesszylinder_FAT |
| 0xA0CC | Komfort_FBD |
| 0xA0CF | Komfort_Tueraussengriff |
| 0xA0E0 | Centerlock_Taster_Verriegeln |
| 0xA0E1 | Centerlock_Taster_Entriegeln |
| 0xA0E2 | DUMMY_1 |
| 0xA0E3 | DUMMY_2 |
| 0xA0E4 | DUMMY_3 |
| 0xA0E5 | DUMMY_4 |
| 0xA0E6 | DUMMY_5 |
| 0xA0E7 | DUMMY_6 |
| 0xA0E8 | DUMMY_7 |
| 0xA0E9 | DUMMY_8 |
| 0xA0EA | DUMMY_9 |
| 0xA0EB | DUMMY_A |
| 0xA0EC | DUMMY_B |
| 0xA0ED | DUMMY_C |
| 0xA0EE | DUMMY_D |
| 0xA0EF | DUMMY_E |
| 0xA0F0 | Fehler_Basestation_Antenne |
| 0xA0F1 | Fehler_TRSP_Page3 |
| 0xA0F2 | Fehler_Typ_Nachschluessel |
| 0xA0F3 | Fehler_TRSP_Cryptodaten |
| 0xA0F4 | DUMMY_F |
| 0xA0F5 | DUMMY_G |
| 0xA0F6 | DUMMY_H |
| 0xA0F7 | DUMMY_I |
| 0xA0F8 | DUMMY_J |
| 0xA0F9 | DUMMY_K |
| 0xA0FA | DUMMY_L |
| 0xA0FB | DUMMY_M |
| 0xA0FC | DUMMY_N |
| 0xA0FD | DUMMY_O |
| 0xA0FE | DUMMY_P |
| 0xA0FF | DUMMY_Q |
| 0xA100 | DME_Lost |
| 0xA101 | EWS4_EEPROM_CRC_FEHLER |
| 0xA102 | EWS4_0xA102 |
| 0xA103 | EWS4_0xA103 |
| 0xA104 | EWS4_0xA104 |
| 0xA105 | EWS4_FSC_FEHLER |
| 0xA106 | EWS4_Random_FEHLER |
| 0xA107 | EWS4_0xA107 |
| 0xA108 | EWS4_0xA108 |
| 0xA109 | EWS4_0xA109 |
| 0xA10A | EWS4_0xA10A |
| 0xA10B | EWS4_CalcTo_FEHLER |
| 0xA10C | EWS4_ZUSTAND_FEHLER |
| 0xA110 | ELV_SW_CAS_Fehler_1 |
| 0xA111 | ELV_HW_CAS_Fehler_1 |
| 0xA112 | ELV_SG_HW_Lenkschloss_Fehler |
| 0xA113 | ELV_SG_Sensor_Fehler |
| 0xA114 | ELV_SG_Kommunikations_Fehler |
| 0xA115 | ELV_SG_Ablauf_Fehler_1 |
| 0xA116 | ELV_SG_Abbruch_Fehler |
| 0xA117 | ASW_SW_CAS_Fehler_2 |
| 0xA118 | ASW_Signalerkennung_Geschwindigkeit_Fehler |
| 0xA119 | ELV_HW_CAS_Fehler_3 |
| 0xA11A | ELV_Hsd_Fehler |
| 0xA11B | ELV_Lsd_Fehler |
| 0xA11C | FLAG_NOT_ALLOWED |
| 0xA11D | ASW_KL30_Fehler |
| 0xA11E | ELV_P_Sternpunkt_Fehler |
| 0xA11F | ELV_M_Sternpunkt_Fehler |
| 0xA120 | KL30g_Kurzschluss |
| 0xA121 | Treiber_LED_KS |
| 0xA122 | Treiber_VCC12_KS |
| 0xA123 | Treiber_VCC34_KS |
| 0xA124 | Fehler_Klemmenstate |
| 0xA125 | DUMMY_W |
| 0xA126 | DUMMY_X |
| 0xA127 | DUMMY_Y |
| 0xA128 | DUMMY_Z |
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
| F_UWB_ERW | nein |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 90 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9400 | CAN_CONTROLLER |
| 0x9304 | EEPROM_CRC_Info |
| 0x9305 | Unterspannung_SG_Info |
| 0x9306 | Ueberspannung_SG_Info |
| 0x9404 | Unplausibilitaet_SG_Spannung_Info |
| 0x9405 | Unplausibilitaet_Bremslicht_Info |
| 0x9406 | Unplausibilitaet_P_N_Info |
| 0x9504 | ZAS_Hall_3_Position_Unstabil |
| 0x9604 | Keine_Antwort_auf_KISI_aktiv_Info |
| 0x9605 | Keine_Antwort_auf_KISI_deakt_Info |
| 0x9804 | DVD_in_Wiederholsperre_Info |
| 0x9805 | DVDR_in_Wiederholsperre_Info |
| 0x9806 | PSD_in_Wiederholsperre_Info |
| 0x9807 | PSDR_in_Wiederholsperre_Info |
| 0x9808 | PM_in_Wiederholsperre_Info |
| 0x9809 | Keine_Bestaet_Kindersich_DVD_Info |
| 0x980A | Keine_Bestaet_Kindersich_DVDR_Info |
| 0x980B | DVD_bestaet_ZV_Aenderung_nicht_Info |
| 0x980C | DVDR_bestaet_ZV_Aenderung_nicht_Info |
| 0x980D | PSD_bestaet_ZV_Aenderung_nicht_Info |
| 0x980E | PSDR_bestaet_ZV_Aenderung_nicht_Info |
| 0x980F | PM_bestaet_ZV_Aenderung_nicht_Info |
| 0x9810 | ZV_RDU_ANFORDERUNG |
| 0x9904 | Fehler_TRSP_Initialisierung |
| 0x9905 | Fehler_Wert_TRSP_Initdone |
| 0x9906 | Fehler_TRSP_Kommunikation |
| 0x9907 | Gesperrter_Schluessel |
| 0x9908 | TRSP_Nicht_Zugehoerig |
| 0x9909 | Kein_TRSP_ID_Erkannt |
| 0x990A | Nachlauf_EWS_Aktiv |
| 0x990B | TRSP_Cryptodaten_Fehler |
| 0x9920 | DUMMY_INFO_9920 |
| 0x9921 | DUMMY_INFO_9921 |
| 0x9923 | DUMMY_INFO_9923 |
| 0x9924 | DUMMY_INFO_9924 |
| 0x9925 | DUMMY_INFO_9925 |
| 0x9A04 | ASW_SW_Info_Fehler_1 |
| 0x9A05 | ASW_HW_Info_Fehler_1 |
| 0x9A06 | ASW_HW_Info_Fehler_2 |
| 0x9A07 | ASW_HW_Info_Fehler_3 |
| 0x9A08 | ELV_KS_Info_Fehler_1  |
| 0x9A09 | ASW_KS_Info_Fehler_2 |
| 0x9A0A | ASW_SPG_Info_Fehler |
| 0x9A0B | ELV_SG_STM_Timing_Info_Fehler |
| 0x9A0C | ASW_CAN_Signal_Info_Fehler |
| 0x9A0D | ELV_SG_sonstiger_Info_Fehler |
| 0x9A0E | ELV_Lenksäule_verspannt_Info_Fehler |
| 0x9A0F | ELV_CAS_ESC_Counter_Info_Fehler |
| 0x9A10 | ELV_externer_WatchDog_Info_Fehler |
| 0x9A11 | ASW_CAN_Bus_Info_Fehler |
| 0x9A12 | ASW_Speed_Info_Fehler |
| 0x9A13 | ASW_ROM_Info_Fehler |
| 0x9A14 | ELV_SG_Info_Fehler |
| 0x9A15 | ELV_Lsd_Info_Fehler |
| 0x9A16 | ELV_SG_ ESC_Counter_Info_Fehler |
| 0x9A17 | ASW_CCM15_KlStrg_Info_Fehler |
| 0x9A18 | ASW_Fatal_Info_Fehler |
| 0x9A19 | ELV_SG_Kommunikation_Timeout_Info_Fehler |
| 0x9A1A | ELV_Kommunikation_Inhalt_Info_Fehler |
| 0x9A1B | ELV_KBUS_Timeout_Control_Info_Fehler |
| 0x9A1C | ASW_CAS_Montagemode |
| 0x9A1D | PLL_NOT_DEACTIVE |
| 0x9A1E | INF_9A1E |
| 0x9A1F | INF_9A1F |
| 0x9A20 | CAS_Awake_Quelle_IO |
| 0x9A21 | CAS_Awake_Quelle_Klstrg |
| 0x9A22 | CAS_Awake_Quelle_ZV |
| 0x9A23 | CAS_Awake_Quelle_FH |
| 0x9A24 | CAS_Awake_Quelle_FBD |
| 0x9A25 | CAS_Awake_Quelle_CA |
| 0x9A26 | CAS_Awake_Quelle_Trsp |
| 0x9A27 | CAS_Awake_Quelle_Trsp2 |
| 0x9A28 | CAS_Awake_Quelle_EE |
| 0x9A29 | CAS_Awake_Quelle_Diag |
| 0x9A2A | CAS_Awake_Quelle_Tester |
| 0x9A2B | CAS_Awake_Quelle_Init |
| 0x9A2C | CAS_Awake_Quelle_FB_Leitung_Offen |
| 0x9A2D | CAS_Awake_Quelle_Sleeptimer_Short |
| 0x9A2E | CAS_Awake_Quelle_Sleeptimer_FH |
| 0x9A2F | CAS_Awake_Quelle_Sleeptimer_Long |
| 0x9A30 | CAS_WakeUp_Quelle_Init |
| 0x9A31 | CAS_WakeUp_Quelle_S_CAN |
| 0x9A32 | CAS_WakeUp_Quelle_HOTEL |
| 0x9A33 | CAS_WakeUp_Quelle_FBD |
| 0x9A34 | CAS_WakeUp_Quelle_KBUS |
| 0x9A35 | CAS_WakeUp_Quelle_Reserved |
| 0x9A36 | CAS_WakeUp_Quelle_Hall_4 |
| 0x9A37 | CAS_WakeUp_Quelle_Hall_3 |
| 0x9A38 | CAS_WakeUp_Quelle_CLT |
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
| F_UWB_ERW | nein |

<a id="table-key-mode-befehle"></a>
### KEY_MODE_BEFEHLE

Dimensions: 8 rows × 3 columns

| WERT | NAME | TEXT |
| --- | --- | --- |
| 0x00 | RISC_EN_DATA | Datenuebertragung CAS &lt;&gt; RISC |
| 0x01 | RISC_EN_CHARGE | RISC in dem Accu-Ladezustand |
| 0x02 | RISC_EN_BATT | Batteriespannung lesen |
| 0x03 | RISC_EN_DIAG | Daten fuer Diagnose berechnen |
| 0x04 | START_AUTH_DIAG | Start der Authentisierung mit Diagnose-Daten, Schluessel im Transponder Mode |
| 0x05 | START_AUTH_CAS | Start der Authentisierung mit CAS Daten, Schluessel im Transponder Mode |
| 0x06 | RF_FIELD_OFF | Schaltet die Versorgung des Transporders aus |
| 0x07 | RISC_EN_ST_KEY | STATUS_KEY vom Starc aktualisiert |

<a id="table-elv-state"></a>
### ELV_STATE

Dimensions: 26 rows × 2 columns

| WERT | NAME |
| --- | --- |
| 0x00 | M_ELV_START_UP |
| 0x01 | M_ELV_GET_IDENT |
| 0x02 | M_ELV_LOCKED |
| 0x03 | M_ELV_HW_CHECK |
| 0x04 | M_ELV_UNLOCK_CONDITION |
| 0x05 | M_ELV_WAIT_FOR_LOCK_STATUS |
| 0x06 | M_ELV_DETECT_ERROR_UNLOCK |
| 0x07 | M_ELV_NEW_TRIGGER_UNLOCK |
| 0x08 | M_ELV_CHECK_CONTROL_UNLOCK |
| 0x09 | M_ELV_SEND_UNLOCK |
| 0x0A | M_ELV_SAVE_UNLOCK_INFO |
| 0x0B | M_ELV_SEND_STATUS_REQ_UNL |
| 0x0C | M_ELV_WAIT_FOR_ST_REQ_UNL |
| 0x10 | M_ELV_UNLOCKED |
| 0x20 | M_ELV_CK_SECOND_EVENT |
| 0x30 | M_ELV_LOCK_CONDITION |
| 0x40 | M_ELV_WAIT_FOR_UNLOCK_STATUS |
| 0x50 | M_ELV_DETECT_ERROR_LOCK |
| 0x60 | M_ELV_NEW_TRIGGER_LOCK |
| 0x70 | M_ELV_CHECK_CONTROL_LOCK |
| 0x80 | M_ELV_SEND_LOCK |
| 0x90 | M_ELV_SAVE_LOCK_INFO |
| 0xA0 | M_ELV_WAIT_FOR_POWER_OFF |
| 0xB0 | M_ELV_SEND_STATUS_REQ_LOCK |
| 0xC0 | M_ELV_WAIT_FOR_ST_REQ_LOCK |
| 0xF0 | M_ELV_WORST_CASE |

<a id="table-ews4-key-state"></a>
### EWS4_KEY_STATE

Dimensions: 18 rows × 3 columns

| WERT | NAME | TEXT |
| --- | --- | --- |
| 0x00 | KEY_READY | KEY_READY |
| 0x5B | WAIT_FIRST_AUT | WAIT_FIRST_AUT |
| 0x5D | SEND_RPLY_KEY | SEND_RPLY_KEY |
| 0x5E | RND_KEY | RND_KEY |
| 0x66 | COMPRESS_KEY | COMPRESS_KEY |
| 0x77 | CALC_KEY | CALC_KEY |
| 0x8B | CHECK_FSC_KEYREADY | CHECK_FSC_KEYREADY |
| 0x8D | CHECK_FSC | CHECK_FSC |
| 0x8E | CHECK_FSC_UNLOCKED | CHECK_FSC_UNLOCKED |
| 0x9B | WAIT_FSC_KEYREADY | WAIT_FSC_KEYREADY |
| 0x9D | WAIT_FSC | WAIT_FSC |
| 0x9E | WAIT_FSC_UNLOCKED | WAIT_FSC_UNLOCKED |
| 0xAA | CALC_FACTOR | CALC_FACTOR |
| 0xBB | WAIT_WR_RND | WAIT_WR_RND |
| 0xCC | INIT_RND2 | INIT_RND2 |
| 0xDD | INIT_RND1 | INIT_RND1 |
| 0xEE | START_RND | START_RND |
| 0xFF | KEY_STATE_CLEARED | KEY_STATE_CLEARED |

<a id="table-steuern-ews4-mode"></a>
### STEUERN_EWS4_MODE

Dimensions: 3 rows × 4 columns

| WERT | NAME | TEXT | DATA_LENGTH |
| --- | --- | --- | --- |
| 0x01 | LOCK_SERVER_SK | LOCK_SERVER_SK | 0 |
| 0x02 | WRITE_SERVER_SK | WRITE_SERVER_SK | 16 |
| 0xFF | UNKNOWN_MODE | UNKNOWN_MODE | 0 |

<a id="table-rdu-number"></a>
### RDU_NUMBER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normal Operation |
| 1 | Nicht ausgeführt: CAN Signal ungültig |
| 2 | Nicht ausgeführt: Fahrzeug fährt |
| 4 | Nicht ausgeführt: Motor startet oder Wiederholsperre aktiv |
| 8 | Nicht ausgeführt: CAS Kodierung |
