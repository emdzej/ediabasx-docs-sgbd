# cas_reset.prg

- Jobs: [138](#jobs)
- Tables: [20](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CAS E_65 |
| ORIGIN | Martin Kaltenbrunner BMW EE-52   |
| REVISION | 0.35 |
| AUTHOR | Mikhail Vaisman/Werner Hoffmann/Johannes Lohberger Siemens AT BE AS CS6 SW |
| COMMENT | Keine Bemerkung |
| PACKAGE | 1.01 |
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
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
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
- [SG_VARIANTE_LESEN](#job-sg-variante-lesen) - Auslesen der SG-Variante auf Basis des Jobs Hardware Referenz lesen KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [STATUS_CAS_DIAGNOSE](#job-status-cas-diagnose) - All Inputs Read KWP2000: $30 InputOutputControlByLocalIdentifier LocalIdentifier=0x01 $01 ReportCurrentState Modus   : Default
- [STEUERN_CAS_DIAGNOSE](#job-steuern-cas-diagnose) - Schreibt 6 Byte "Digital Outputs" KWP2000: $30 InputOutputControlByLocalIdentifier LocalIdentifier=$02 $07 ShortTermAdjustment Modus  : Default
- [STATUS_ISN](#job-status-isn) - 4 Byte des ISN KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $01 Modus   : Default
- [STATUS_MECHANISCHER_SCHLUESSELCODE](#job-status-mechanischer-schluesselcode) - 5 Byte des Mechanischer Schluesselcode KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $02 Modus   : Default
- [STATUS_SCHLUESSEL_FREQUENZ](#job-status-schluessel-frequenz) - Frequenz des Schluessels KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $03 Modus   : Default
- [STATUS_PROG_LOCATION_DATUM](#job-status-prog-location-datum) - Ort und Datum der ECU-Programmierung KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $04 Modus   : Default
- [STATUS_ZV_AUTHENTISIERUNG](#job-status-zv-authentisierung) - aktueller Status "ZV-Authentisierung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $05 Modus   : Default
- [STATUS_TRSP_INIT](#job-status-trsp-init) - aktueller Status "TRSP, Init-Kennung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $06 Modus   : Default
- [STATUS_TRSP_FAHRZYKLUSZAEHLER](#job-status-trsp-fahrzykluszaehler) - aktueller Status "TRSP, Fahrzykluszaehler" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $07 Modus   : Default
- [STATUS_CAS_INIT_KENNUNG](#job-status-cas-init-kennung) - aktueller Status "CAS, Init-Kennung" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $08 Modus   : Default
- [STATUS_BDM_SPERREN](#job-status-bdm-sperren) - BDM-Sperren-Status Lesen KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $09 Modus   : Default
- [STATUS_DME_RINGBUFFER](#job-status-dme-ringbuffer) - aktueller Status "DME-RingBuffer" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0A Modus   : Default
- [STATUS_ZVFH_RINGBUFFER](#job-status-zvfh-ringbuffer) - aktueller Status "ZV/FH-Ringpuffer" KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0B Modus   : Default
- [STATUS_FBD_TELEGRAMM](#job-status-fbd-telegramm) - letztes FBD-Telegramm KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0C Modus   : Default
- [STATUS_PA_TELEGRAMM](#job-status-pa-telegramm) - letztes PA-Telegramm KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0D Modus   : Default
- [STATUS_ICT_BYTE](#job-status-ict-byte) - Internal Circuit Test Byte (Siemens Data) KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0E Modus   : Default
- [STATUS_MLFB](#job-status-mlfb) - MLFB Data Siemens KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $0F Modus   : Default
- [STATUS_SCHLUESSEL_DATEN](#job-status-schluessel-daten) - Auslesen der SCHLUESSELDATEN KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $10...$19 Modus   : Default
- [STATUS_BASESTATION](#job-status-basestation) - Auslesen der Basestation Status KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $25 Modus   : Default
- [STATUS_AKTUELL_SCHLUESSEL](#job-status-aktuell-schluessel) - aktuelle Schluessel KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $27 Modus   : Default
- [STATUS_TRANSPONDER_PAGE](#job-status-transponder-page) - Transponder Page KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2A Modus   : Default
- [STATUS_SET_PAGE_TRSP](#job-status-set-page-trsp) - Page TRSP KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2D Modus   : Default
- [STATUS_XTRSP_TEST_DATA](#job-status-xtrsp-test-data) - Test Data KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $2F Modus   : Default
- [STATUS_XTRSP](#job-status-xtrsp) - XTRSP Status KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $30 Modus   : Default
- [STATUS_TRSP_DATEN](#job-status-trsp-daten) - aktuelle Transponder-Daten KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $40-$49 Modus   : Default
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
- [STATUS_BOS_CC_DATEN](#job-status-bos-cc-daten) - Lesen von 32 Byte "BOS_CC-Daten" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1016-1018 Modus   : Default
- [STATUS_FSD_DATEN](#job-status-fsd-daten) - Lesen von 32 Byte "FSD-Daten" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=$1019-101A Modus   : Default
- [STATUS_FAHRZEUGAUFTRAG](#job-status-fahrzeugauftrag) - Liest 16 Byte "Fahrzeugauftrag" KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=3F00...3F13 Modus   : Default
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default
- [STEUERN_ISN](#job-steuern-isn) - Schreibt  4Byte "ISN" und kopiert diesen auf beide  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $01 Modus  : Default
- [STEUERN_MECH_SCHLUESSELCODE](#job-steuern-mech-schluesselcode) - Schreibt 10 Byte "mechan. Schluessel-Code"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $02 Modus  : Default
- [STEUERN_SCHLUESSEL_FREQUENZ](#job-steuern-schluessel-frequenz) - Schreibt 1 Byte "Schluessel-Frequenz"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $03 Modus  : Default
- [STEUERN_PROG_LOCATION_DATUM](#job-steuern-prog-location-datum) - Schreibt 3 Byte "Programmier-Ort/Datum"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $04 Modus  : Default
- [STEUERN_ZV_AUTHENTISIERUNG](#job-steuern-zv-authentisierung) - Schreibt 4 Byte "ZV-Authentisierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $05 Modus  : Default
- [STEUERN_TRANSPONDERKENNUNG](#job-steuern-transponderkennung) - Schreibt 3 Byte "Transponder-Aktivierung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $06 Modus  : Default
- [STEUERN_TRSP_FAHRZYKLUSZAEHLER](#job-steuern-trsp-fahrzykluszaehler) - Schreibt 4 Byte "Transponder-Fahrzykluszaehler"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $07 Modus  : Default
- [STEUERN_CAS_INIT_KENNUNG](#job-steuern-cas-init-kennung) - Schreibt 3 Byte "Initialisierungs-Kennung"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $08 Modus  : Default
- [STEUERN_BDM_SPERREN](#job-steuern-bdm-sperren) - BDM Sperren (only in special mode with BDM interface!!!)  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $09 Modus  : Default
- [STEUERN_DME_RINGBUFFER](#job-steuern-dme-ringbuffer) - Schreibt 31 Byte "DME-Ringpuffer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0A Modus  : Default
- [STEUERN_ZVFH_RINGBUFFER](#job-steuern-zvfh-ringbuffer) - Schreibt 64+1 Byte "ZV/FH-Ringpuffer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0B Modus  : Default
- [STEUERN_ICT_BYTE](#job-steuern-ict-byte) - Internal Circuit Byte Schreiben  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $0E Modus  : Default
- [STEUERN_SCHLUESSELDATEN](#job-steuern-schluesseldaten) - Schreibt 17 Byte "Schluessel-Daten"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $10...$19 Modus  : Default
- [STEUERN_SCHLUESSEL_GESPERRT](#job-steuern-schluessel-gesperrt) - Schreibt 1 Byte "Schluessel-Sperre"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $20 Modus  : Default
- [STEUERN_SCHLUESSEL_FREIGEBEN](#job-steuern-schluessel-freigeben) - Schreibt 1 Byte "Schluessel-Nummer"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $21 Modus  : Default
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
- [CAS_INIT_OHNE_AUTHENTICATION](#job-cas-init-ohne-authentication) - Normal-&gt;Jungfraeulich ohne Authentication KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $24 Modus  : Default
- [C_C_AUFTRAG_CAS](#job-c-c-auftrag-cas) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default
- [C_C_LESEN_CAS](#job-c-c-lesen-cas) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default
- [C_C_SCHREIBEN_CAS](#job-c-c-schreiben-cas) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default

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
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

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
| STATUS_CRC_EEPROM | unsigned char | Bereich 0=incorrect 1=correct Byte00, Bit2 |
| STATUS_CRC_FLASH | unsigned char | Bereich 0=incorrect 1=correct Byte00, Bit3 |
| IN_ZAS_SSTADISC | unsigned char | Bereich 0/1 Byte01, Bit0 |
| IN_ZAS_SSTBDISC | unsigned char | Bereich 0/1 Byte01, Bit1 |
| IN_ZAS_RASTDISC | unsigned char | Bereich 0/1 Byte01, Bit2 |
| IN_ZAS_EJECTDISC | unsigned char | Bereich 0/1 Byte01, Bit3 |
| IN_BIMAG_STATUSDISC | unsigned char | Bereich 0/1 Byte01, Bit4 |
| IN_RCGLIED_DISC | unsigned char | Bereich 0/1 Byte01, Bit5 |
| IN_VKL3KMH_DISC | unsigned char | Bereich 0/1 Byte01, Bit6 |
| IN_VGR3KMH_DISC | unsigned char | Bereich 0/1 Byte01, Bit7 |
| IN_ZAS_BLSDISC | unsigned char | Bereich 0/1 Byte02, Bit0 |
| IN_EGS_PNDISC | unsigned char | Bereich 0/1 Byte02, Bit1 |
| IN_ER_DISC | unsigned char | Bereich 0/1 Byte02, Bit2 |
| IN_VR_DISC | unsigned char | Bereich 0/1 Byte02, Bit3 |
| IN_HKL_AUFDISC | unsigned char | Bereich 0/1 Byte02, Bit4 |
| IN_MHK_ZUDISC | unsigned char | Bereich 0/1 Byte02, Bit5 |
| IN_HTLSTLG_EINDISC | unsigned char | Bereich 0/1 Byte02, Bit6 |
| IN_FB_MOTFERNSTARTDISC | unsigned char | Bereich 0/1 Byte02, Bit7 |
| IN_DFAHL_DIAGDISC | unsigned char | Bereich 0/1 Byte03, Bit0 |
| IN_RESERVE1_DISC | unsigned char | Bereich 0/1 Byte03, Bit1 |
| IN_PCAN_NERRDISC | unsigned char | Bereich 0/1 Byte03, Bit2 |
| IN_SCAN_NERRDISC | unsigned char | Bereich 0/1 Byte03, Bit3 |
| IN_PA_KBUSRXDDISC | unsigned char | Bereich 0/1 Byte03, Bit4 |
| IN_TRSP_DATADISC | unsigned char | Bereich 0/1 Byte03, Bit5 |
| IN_FZV_DATADISC | unsigned char | Bereich 0/1 Byte03, Bit6 |
| RESERVE_BYTE3_BIT7 | unsigned char | Bereich 0/1 Byte03, Bit7 |
| STATUS_RING_DATA_3 | unsigned char | Bereich 0-255 Byte04 |
| IN_KL30L_DIAGDISC | real | Byte05 |
| IN_KL30E_DIAGDISC | real | Einheit: Volt Byte06 |
| IN_KL15_DIAG1DISC | real | Einheit: Volt Byte07 |
| IN_KL15_DIAG2DISC | real | Einheit: Volt Byte08 |
| IN_KL15_DIAG3DISC | real | Einheit: Volt Byte09 |
| IN_KL15_DIAG4DISC | real | Einheit: Volt Byte10 |
| IN_KL15_WAKEUPDISC | real | Einheit: Volt Byte11 |
| IN_KL15_WUPACCDISC | real | Einheit: Volt Byte12 |
| IN_KL50E_DIAGDISC | real | Einheit: Volt Byte13 |
| IN_KL50__DIAGDISC | real | Einheit: Ampere Byte14 |
| KEY_STATUS_0 | unsigned char | Bereich 0..255 Byte15 |
| KEY_STATUS_1 | unsigned char | Bereich 0..255 Byte16 |
| KEY_STATUS_2 | unsigned char | Bereich 0..255 Byte17 |
| KEY_STATUS_3 | unsigned char | Bereich 0..255 Byte18 |
| KEY_STATUS_4 | unsigned char | Bereich 0..255 Byte19 |
| KEY_STATUS_5 | unsigned char | Bereich 0..255 Byte20 |
| STAT_KEY_NO_IDENTIFIER | unsigned char | Bereich 0/1 Byte16, Bit5 |
| STAT_KEY_WRONG_FREQUENCY | unsigned char | Bereich 0/1 Byte19, Bit3 |
| STAT_KEY_WRONG_MECH_CODE | unsigned char | Bereich 0/1 Byte19, Bit5 |
| STAT_KEY_NO_POCKET_KEY | unsigned char | Bereich 0/1 Byte19, Bit6 |
| STAT_KEY_NO_FBD_PA_KEY | unsigned char | Bereich 0/1 Byte19, Bit7 |
| FBD_QUELLE | unsigned char | Bereich 0..255 Byte21 |
| FBD_PERSONAL_NR | unsigned char | Bereich 0..255 Byte22 |
| FBD_KEY_NR | unsigned char | Bereich Byte23 |
| FBD_QUANT | unsigned char | Bereich 0-255 Byte24 |
| FBD_QUANT_MAX | unsigned char | Bereich 0-255 Byte25 |
| FBD_QUANT_MIN | unsigned char | Bereich 0-255 Byte26 |
| FBD_MFS_START | unsigned char | Bereich 0-255 Byte27 |
| FBD_MFS_STOPP | unsigned char | Bereich 0-255 Byte28 |
| STAT_RADDREHZAHL | unsigned int | Signal STATE_DFAHL, Bereich 0-65535 Byte29-30 |
| ZAS_BEDIENSPERRE | unsigned char | Bereich 0-1 Byte31 |
| ZAS_SSTAB | unsigned char | Bereich 0-1 Byte31 |
| ZAS_SST | unsigned char | Bereich 0-1 Byte31 |
| ZAS_EJECT | unsigned char | Bereich 0-1 Byte31 |
| ZAS_FLANKE | unsigned char | Bereich 0-1 Byte31 |
| ZAS_NOTAUS | unsigned char | Bereich 0-1 Byte31 |
| ZAS_KOMFORTAUS | unsigned char | Bereich 0-1 Byte31 |
| ZAS_VERRASTET | unsigned char | Bereich 0-1 Byte31 |
| ZAS_ALSP | unsigned char | Bereich 0-1 Byte32 |
| ZAS_AWSP | unsigned char | Bereich 0-1 Byte32 |
| ZAS_AZSP | unsigned char | Bereich 0-1 Byte32 |
| ZAS_PDISC | unsigned char | Bereich 0-1 Byte32 |
| ZAS_NCAN | unsigned char | Bereich 0-1 Byte32 |
| ZAS_PCAN | unsigned char | Bereich 0-1 Byte32 |
| ZAS_NMOT | unsigned char | Bereich 0-3 Byte32 |
| ZAS_BLS | unsigned char | Bereich 0-1 Byte33 |
| ZAS_VFZGAZSP | unsigned char | Bereich 0-1 Byte33 |
| ZAS_VFZGNOTST | unsigned char | Bereich 0-1 Byte33 |
| ZAS_VFZGHW | unsigned char | Bereich 0-1 Byte33 |
| ZAS_FREIGABE | unsigned char | Bereich 0-1 Byte33 |
| ZAS_FERNSTART | unsigned char | Bereich 0-1 Byte33 |
| ZAS_SWRCGLFENSTER | unsigned char | Bereich 0-1 Byte33 |
| ZAS_PA_AKTIV | unsigned char | Bereich 0-1 Byte33 |
| ZAS_BLS_DEFEKT | unsigned char | Bereich 0-1 Byte34 |
| ZAS_SIGNATUR_DUMMY1 | unsigned char | Bereich 0-127 Byte34 |
| ZAS_SIGNATUR_DUMMY2 | unsigned char | Bereich 0-255 Byte35 |
| ZAS_SIGNATUR_DUMMY3 | unsigned char | Bereich 0-255 Byte36 |
| S_PE_KAPFAT | unsigned char | Bereich 0-1 Byte37 |
| S_PE_KAPFATH | unsigned char | Bereich 0-1 Byte37 |
| S_PE_KAPBFT | unsigned char | Bereich 0-1 Byte37 |
| S_PE_KAPBFTH | unsigned char | Bereich 0-1 Byte37 |
| S_PE_ERFAT | unsigned char | Bereich 0-1 Byte37 |
| S_PE_ERFATH | unsigned char | Bereich 0-1 Byte37 |
| S_PE_ERBFT | unsigned char | Bereich 0-1 Byte37 |
| S_PE_ERBFTH | unsigned char | Bereich 0-1 Byte37 |
| S_PE_VRFAT | unsigned char | Bereich 0-1 Byte38 |
| S_PE_VRFATH | unsigned char | Bereich 0-1 Byte38 |
| S_PE_VRBFT | unsigned char | Bereich 0-1 Byte38 |
| S_PE_VRBFTH | unsigned char | Bereich 0-1 Byte38 |
| S_PA_IDGPRIO | unsigned char | Bereich 0-15 Byte38 |
| S_PE_FT_AUTH | unsigned char | Bereich 0-1 Byte39 |
| S_PE_FTH_AUTH | unsigned char | Bereich 0-1 Byte39 |
| S_PE_BFT_AUTH | unsigned char | Bereich 0-1 Byte39 |
| S_PE_BFTH_AUTH | unsigned char | Bereich 0-1 Byte39 |
| S_PE_HK_AUTH | unsigned char | Bereich 0-1 Byte39 |
| S_PE_ER | unsigned char | Bereich 0-1 Byte39 |
| S_PE_VR | unsigned char | Bereich 0-1 Byte39 |
| Z_PA_TRSP | unsigned char | Bereich 0-1 Byte39 |
| S_PE_STATE | unsigned char | Bereich 0-255 Byte40 |
| S_PG_STATE | unsigned char | Bereich 0-255 Byte41 |
| S_HK_STATE | unsigned char | Bereich 0-255 Byte42 |
| S_AUTH_STATE | unsigned char | Bereich 0-255 Byte43 |
| S_SEARCH_STATE | unsigned char | Bereich 0-255 Byte44 |
| STAT_KL_R | unsigned char | Status_Klemme_R (00=Kl R aus,01=Kl R ein), Bereich 0-3 Byte45, Bit 0-1 |
| STAT_KL_15 | unsigned char | Status_Klemme_15 (00=Kl 15 aus,01=Kl 15 ein), Bereich 0-3 Byte45, Bit 2-3 |
| STAT_KL_50 | unsigned char | Status_Klemme_50 (00=Kl 50 aus,01=Kl 50 ein), Bereich 0-3 Byte45, Bit 4-5 |
| STAT_KEY_VALID | unsigned char | Status_Schlüssel_Gueltig (00=no key,01=valid key,10=no valid key), Bereich 0-3 Byte45, Bit 6-7 |
| NO_KEY | unsigned char | Schluesselnummer, Bereich 0-15 Byte46, Bit 0-3 |
| STAT_KEY_TYP | unsigned char | Status_Schluessel_Typ (0=no key,2=Pocket,4=Remote,5=PA), Bereich 0-15 Byte46, Bit 4-7 |
| STAT_KEY_PLGD | unsigned char | Status_Schluessel_Steckt (00=no key,01=key plugged), Bereich 0-3 Byte47, Bit 0-1 |
| STAT_VHIM | unsigned char | Status_Wegfahrsperre (01=gesperrt,10=frei), Bereich 0-3 Byte47, Bit 2-3 |
| ST_LOKG_STCO | unsigned char | Bereich 0-3 Byte47 |
| STAT_KEYLOCK | unsigned char | Status_Keylock (00=not active,01=active), Bereich 0-3 Byte47, Bit 6-7 |
| POS_ID_PU | unsigned char | Position_ID_Geber (00=Kein IDG,01=IDG im Innenraum,10=IDG ausserhalb erkannt), Bereich 0-3 Byte48, Bit 0-1 |
| STAT_PSVA_ACV | unsigned char | Status_Passive-Access_Aktiv (00=not active,01=active), Bereich 0-3 Byte48, Bit 2-3 |
| ALIV_KL | unsigned char | Alive_Klemme, Bereich 0-15 Byte49, Bit 0-3 |
| CHKSM_KL | unsigned char | Checksumme_Klemme, Bereich 0-15 Byte49, Bit 4-7 |
| STAT_CLSY | unsigned char | Status_Zentralverriegelung (s. LH), Bereich 0-15 Byte50, Bit 0-3 |
| CTR_CLSY | unsigned char | Steuerung_Zentralverriegelung (s. LH), Bereich 0-15 Byte50, Bit 4-7 |
| STAT_DSW_DRD | unsigned char | Status_Tuerkontakt_FAT (00=geschlossen,01=offen), Bereich 0-3 Byte51, Bit 0-1 |
| STAT_DSW_PSD | unsigned char | Status_Tuerkontakt_BFT (00=geschlossen,01=offen), Bereich 0-3 Byte51, Bit 2-3 |
| STAT_DSW_DVDR | unsigned char | Status_Tuerkontakt_FATH (00=geschlossen,01=offen), Bereich 0-3 Byte51, Bit 4-5 |
| STAT_DSW_PSDR | unsigned char | Status_Tuerkontakt_BFTH (00=geschlossen,01=offen), Bereich 0-3 Byte51, Bit 6-7 |
| STAT_CT_BTL | unsigned char | Status_Kontakt_Heckklappe (00=geschlossen,01=offen), Bereich 0-3 Byte52, Bit 0-1 |
| STAT_CT_BON | unsigned char | Status_Kontakt_Motorhaube (00=geschlossen,01=offen), Bereich 0-3 Byte52, Bit 2-3 |
| STAT_HOTM | unsigned char | Status_Hotelstellung (00=nicht aktiv,01=aktiv), Bereich 0-3 Byte52, Bit 4-5 |
| STAT_PUBU_CLSY | unsigned char | Status_Taster_Zentralverriegelung (00= nicht betaetigt,01=entriegeln,10=verriegeln), Bereich 0-3 Byte52, Bit 6-7 |
| AUTH_CLSY_0 | unsigned char | Authentisierung_Zentralverriegelung, Bereich 0-255 Byte53 |
| AUTH_CLSY_1 | unsigned char | Bereich 0-255 Byte54 |
| AUTH_CLSY_2 | unsigned char | Bereich 0-255 Byte55 |
| AUTH_CLSY_3 | unsigned char | Bereich 0-255 Byte56 |
| STAT_DREHZAHL_MOTOR | unsigned int | Bereich 0-65535 Signal RPM_ENGINE, Byte57-58 |
| STAT_GANG_GETRIEBE | unsigned char | Signal ST_GR_GRB, Bereich 0-15 (s. LH) Byte59 |
| STAT_KONTAKT_BREMSPEDAL | unsigned char | Signal ST_CT_BRPD, Bereich 0-3 (s. LH) Byte59 |
| STAT_MOTOR_LAEUFT | unsigned char | Signal ST_ENG_RUN, Bereich 0-3 (s. LH) Byte59 |
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

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
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
| FBD_TELEGRAMM | binary | 11 Byte Byte0-10 |
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
| GUELTIGER_WERT | unsigned char | Bereich 0/1 |
| PROGRAMMIERUNG_FEHLERHAFT | unsigned char | Bereich 0/1 |
| R_W_SEQUENZ_NOCH_NICHT_BEENDET | unsigned char | Bereich 0/1 |
| CKS_FEHLER | unsigned char | Bereich 0/1 |
| ZUGRIFF_VERWEIGERT | unsigned char | Bereich 0/1 |
| FEHLERHAFTE_REIHENFOLGE | unsigned char | Bereich 0/1 |
| BLOCK_IST_ZUGRIFFSGESPERRT | unsigned char | Bereich 0/1 |
| BERECHNUNG_NOCH_NICHT_ABGESCHLOSSEN | unsigned char | Bereich 0/1 |
| INIT_MAL_ERFOLGT | unsigned char | Bereich 0/1 |
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
| DEALER_ORG | binary | "HO-Codierung": Byte0-3 |
| FIRST_REG_DEALER | unsigned char | "Ort" Byte4 |
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
| PAGE_NUMMER | unsigned char | "Page": 0-7,0xFF, "WUP": 0xFE ======&gt; Byte0 |

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
| DEALER_ORG | string | "HO-Codierung" ======&gt; Byte0-3 |
| FIRST_REG_DEALER | unsigned char | "Haendler" ======&gt; Byte4 |
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

<a id="job-cas-init-ohne-authentication"></a>
### CAS_INIT_OHNE_AUTHENTICATION

Normal-&gt;Jungfraeulich ohne Authentication KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $24 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-auftrag-cas"></a>
### C_C_AUFTRAG_CAS

Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default

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

<a id="job-c-c-lesen-cas"></a>
### C_C_LESEN_CAS

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default

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

<a id="job-c-c-schreiben-cas"></a>
### C_C_SCHREIBEN_CAS

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $1000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (60 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [IORTTEXTE](#table-iorttexte) (40 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [KEY_MODE_BEFEHLE](#table-key-mode-befehle) (8 × 3)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 76 rows × 2 columns

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
| ?A0? | ERROR_DIAG_PROT |
| ?A1? | ERROR_SG_ADRESSE |
| ?A2? | ERROR_SG_MAXANZAHL_AIF |
| ?A3? | ERROR_SG_GROESSE_AIF |
| ?A4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?A5? | ERROR_SG_AUTHENTISIERUNG |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 56 rows × 2 columns

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
| 0x55 | BHTC |
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

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
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
| 0x07 | nicht benutzt |
| 0x08 | nicht benutzt |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 60 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xD904 | K_CAN_LOW_SYS, Physikalischer Busfehler D904 |
| 0xD905 | K_CAN_HIGH_SYS                          D905 |
| 0xD906 | GroundShift_SYS                         D906 |
| 0xD907 | CAN_Controller_SYS, Bus off             D907 |
| 0xD93C | Fehlerwert_erhalten_SYS                 D93C |
| 0xD93D | Unplausibles_Signal_SYS                 D93D |
| 0xD93E | Telegramm_Timeout_beim_Emfang_SYS       D93E |
| 0xD93F | Fehler_beim_Emfang_NM_Botschaft_SYS     D93F |
| 0xD940 | Fehlerwert_gesendet_SYS                 D940 |
| 0xD941 | Unplausibles_Signal1_SYS                D941 |
| 0xD942 | Telegramm_Timeout_beim_Senden_SYS       D942 |
| 0xD943 | Fehler_beim_Senden_NM_Botschaft_SYS     D943 |
| 0xE904 | K_CAN_LOW_PER, Physikalischer Busfehler E904 |
| 0xE905 | K_CAN_HIGH_PER                          E905 |
| 0xE906 | GroundShift_PER                         E906 |
| 0xE907 | CAN_Controller_PER, Bus off             E907 |
| 0xE93C | Fehlerwert_erhalten_PER                 E93C |
| 0xE93D | Unplausibles_Signal_PER                 E93D |
| 0xE93E | Telegramm_Timeout_beim_Emfang_PER       E93E |
| 0xE93F | Fehler_beim_Emfang_NM_Botschaft_PER     E93F |
| 0xE940 | Fehlerwert_gesendet_PER                 E940 |
| 0xE941 | Unplausibles_Signal1_PER                E941 |
| 0xE942 | Telegramm_Timeout_beim_Senden_PER       E942 |
| 0xE943 | Fehler_beim_Senden_NM_Botschaft_PER     E943 |
| 0xA0A8 | RAM_CRC_FEHLER                  A0A8 |
| 0xA0AA | BootFlash_CRC_FEHLER            A0AA |
| 0xA0AB | ProgFlash_CRC_FEHLER            A0AB |
| 0xA0AC | SG_Fehler_COP_CM_TRAP           A0AC |
| 0xA0AD | EEPROM_WRITE_FEHLER             A0AD |
| 0xA0AE | Energiesparmodi                 A0AE |
| 0xA0B0 | SG_Eingang_Bremselicht          A0B0 |
| 0xA0B1 | SG_Eingang_P_N                  A0B1 |
| 0xA0B2 | Fehler_CAS_Versorgung           A0B2 |
| 0xA0B3 | Fehler_Ansteurung_Anlasser_KL50 A0B3 |
| 0xA0B4 | Fehler_Motorstart_Anlasserbetrieb A0B4 |
| 0xA0B5 | DFAHL_Kabelbruch                A0B5 |
| 0xA0B8 | Hallsensor_verrastet            A0B8 |
| 0xA0B9 | Hallsensor_eject                A0B9 |
| 0xA0BA | Hallsensor_SSTA                 A0BA |
| 0xA0BB | Hallsensor_SSTB                 A0BB |
| 0xA0BC | Hubmagnet_AZSP                  A0BC |
| 0xA0BD | KL15_Wakeup_Ausgangstreiber     A0BD |
| 0xA0BE | Treiber_KL15_1_FZG_KS           A0BE |
| 0xA0BF | Treiber_KL15_2_FZG_KS           A0BF |
| 0xA0C0 | Treiber_KL15_3_FZG_KS           A0C0 |
| 0xA0C1 | Treiber_KL50L_KS                A0C1 |
| 0xA0C2 | Treiber_KL50E_KS                A0C2 |
| 0xA0C3 | KL15_WUP_ACC_KS                 A0C3 |
| 0xA0C4 | Treiber_KL15_4_FZG_KS           A0C4 |
| 0xA0C8 | Komfort_Schliesszylinder_FAT    A0C8 |
| 0xA0CC | Komfort_FBD                     A0CC |
| 0xA0CF | Komfort_Tueraussengriff         A0CF |
| 0xA0E0 | Centerlock_Taster_Verriegeln    A0E0 |
| 0xA0E1 | Centerlock_Taster_Entriegeln    A0E1 |
| 0xA0F0 | Fehler_Basestation_Antenne      A0F0 |
| 0xA0F1 | Fehler_TRSP_Page3               A0F1 |
| 0xA0F2 | Fehler_Typ_Nachschluessel       A0F2 |
| 0xA0F3 | Fehler_TRSP_Cryptodaten         A0F3 |
| 0xA100 | DME_Lost                        A100 |
| 0xA102 | DME_Drehzahl                    A102 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Km-Stand1 | km | - | unsigned int | - | 8 | 1 | 0 |
| 0xFF | ohne Bedeutung | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 40 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9304 | EEPROM_CRC_FEHLER |
| 0x9305 | Unterspannung_SG_Info |
| 0x9306 | Ueberspannung_SG_Info |
| 0x9404 | Unplausibilitaet_SG_Spannung_Info |
| 0x9405 | Unplausibilitaet_Bremslicht_Info |
| 0x9406 | Unplausibilitaet_P_N_Info |
| 0x9604 | Keine_Antwort_auf_KISI_aktiv_Info |
| 0x9605 | Keine_Antwort_auf_KISI_deakt_Info |
| 0x9804 | DVD_in_Wiederholsperre_Info |
| 0x9805 | DVDR_in_Wiederholsperre_Info |
| 0x9806 | PSD_in_Wiederholsperre_Info |
| 0x9807 | PSDR_in_Wiederholsperre_Info |
| 0x9808 | PM_in_Wiederholsperre_Info |
| 0x9809 | Keine_Bestaetigung_KiSi_DVD_Info |
| 0x980A | Keine_Bestaetigung_KiSi_DVDR_Info |
| 0x980B | DVD_bestaet_ZV_Aenderung_nicht_Info |
| 0x980C | DVDR_bestaet_ZV_Aenderung_nicht_Info |
| 0x980D | PSD_bestaet_ZV_Aenderung_nicht_Info |
| 0x980E | PSDR_bestaet_ZV_Aenderung_nicht_Info |
| 0x980F | PM_bestaet_ZV_Aenderung_nicht_Info |
| 0x9904 | Fehler_TRSP_Initialisierung |
| 0x9905 | Fehler_Wert_TRSP_Initdone |
| 0x9906 | Fehler_TRSP_Kommunikation |
| 0x9907 | Gesperrter_Schluessel |
| 0x9908 | TRSP_Nicht_Zugehoerig |
| 0x9909 | Kein_TRSP_ID_Erkannt |
| 0x990A | Nachlauf_EWS_Aktiv |
| 0x9B04 | Schl01_ausserhalb_Fangbereich_Info |
| 0x9B05 | Schl02_ausserhalb_Fangbereich_Info |
| 0x9B06 | Schl03_ausserhalb_Fangbereich_Info |
| 0x9B07 | Schl04_ausserhalb_Fangbereich_Info |
| 0x9B08 | Schl05_ausserhalb_Fangbereich_Info |
| 0x9B09 | Schl06_ausserhalb_Fangbereich_Info |
| 0x9B0A | Schl07_ausserhalb_Fangbereich_Info |
| 0x9B0B | Schl08_ausserhalb_Fangbereich_Info |
| 0x9B0C | Schl09_ausserhalb_Fangbereich_Info |
| 0x9B0D | Schl10_ausserhalb_Fangbereich_Info |
| 0x9B0E | TH_01_ausserhalb_Fangbereich_Info |
| 0x9B0F | TH_02_ausserhalb_Fangbereich_Info |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | nein |

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
