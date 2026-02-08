# N62_TUE2.PRG

- Jobs: [255](#jobs)
- Tables: [54](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ME9.2.3 fuer N62 mit EWS3 oder CAS  |
| ORIGIN | BMW EA-41 Holger Dieffenbach |
| REVISION | 1.000 |
| AUTHOR | ValleyForge-T.I.S. EA-41 Wieser |
| COMMENT | SGBD fuer ME9.2.3 mit SW 733W4000 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
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
- [_STATUS_BZEINFO](#job-status-bzeinfo) - 0x22401A _STATUS_BZEINFO Infospeicher Batterie Zustands Erkennung (BZE) auslesen Aktivierung: Klemme 15 = EIN Activation:
- [_STATUS_GENINFO](#job-status-geninfo) - 0x22401B _STATUS_GENINFO Infospeicher Generatordiagnose erweitert auslesen Aktivierung: Klemme 15 = EIN Activation:
- [DATA_ID_LESEN](#job-data-id-lesen) - 0x222504 DATA_ID_LESEN Data-ID des SG auslesen Aktivierung: Klemme 15 = EIN Activation:
- [PROGSTAND_LONG_LESEN](#job-progstand-long-lesen) - 0x222504 PROGSTAND_LONG_LESEN Programmstand-Nr. des SG auslesen Aktivierung: Klemme 15 = EIN Activation:
- [IDENT_AIF](#job-ident-aif) - 0x1A80 und 0x23 IDENT_AIF Identdaten und Anwender Informations Felder Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_POWER_DOWN](#job-steuern-power-down) - Anforderung Power Down Mode
- [STATUS_CODIERUNG_BZE](#job-status-codierung-bze) - 0x223230 STATUS_CODIERUNG_BZE Codierung fuer BZE (Batterie Zustands Erkennung) auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_IGR](#job-status-codierung-igr) - 0x223210 STATUS_CODIERUNG_IGR Codierung fuer IGR (Intelligente Generator-Regelung) auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_KAT](#job-status-codierung-kat) - 0x223001 STATUS_CODIERUNG_KAT Codierung fuer Katalysator auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_MIL](#job-status-codierung-mil) - 0x223000 STATUS_CODIERUNG_MIL Codierung fuer MIL (Malfunction Indication Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_OEL](#job-status-codierung-oel) - 0x223200 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_PROTOKOLL](#job-status-codierung-protokoll) - 0x223030 STATUS_CODIERUNG_PROTOKOLL Codierung Protokoll auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_SPA](#job-status-codierung-spa) - 0x223220 STATUS_CODIERUNG_SPA Codierung fuer SPA (Schaltpunktanzeige) auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_VMAX](#job-status-codierung-vmax) - 0x223010 STATUS_CODIERUNG_VMAX Codierung fuer maximale Geschwindigkeit auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CODIERUNG_XENON](#job-status-codierung-xenon) - 0x223211 STATUS_CODIERUNG_XENON Codierung fuer Xenon-Lichtverbau auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_RBMMODE9](#job-status-rbmmode9) - 0x224026 STATUS_RBMMODE9 Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_RBMME1](#job-status-rbmme1) - 0x224029 STATUS_RBMME1 Lesen der RBM-Werte Block1 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_RBMME2](#job-status-rbmme2) - 0x22402A STATUS_RBMME2 Lesen der RBM-Werte Block2 Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VVT_ANSCHLAG](#job-steuern-vvt-anschlag) - 0x312706 STEUERN_VVT_ANSCHLAG Lernen der VVT-Anschlaege Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_VVT_ANSCHLAG](#job-status-vvt-anschlag) - 0x211B STATUS_VVT_ANSCHLAG Status Lernen VVT-Anschlaege Aktivierung: Klemme 15 = EIN Activation:
- [STOP_VVT_ANSCHLAG](#job-stop-vvt-anschlag) - 0x322706 STOP_VVT_ANSCHLAG Ende von Lernen der VVT-Anschlaege Aktivierung: Klemme 15 = EIN Activation:
- [FS_HEX_LESEN](#job-fs-hex-lesen) - 0x210A0000 FS_HEX_LESEN Fehlerspeicher auslesen als Hex Dump Aktivierung: Klemme 15 = EIN Activation:
- [FS_LESEN_LANG](#job-fs-lesen-lang) - 0x210A0000 FS_LESEN_LANG Fehlerspeicher auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_1](#job-steuern-ev-1) - 0x30CB07FF STEUERN_EV_1 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_2](#job-steuern-ev-2) - 0x30CC07FF STEUERN_EV_2 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_3](#job-steuern-ev-3) - 0x30CD07FF STEUERN_EV_3 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_4](#job-steuern-ev-4) - 0x30CE07FF STEUERN_EV_4 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_5](#job-steuern-ev-5) - 0x30CF07FF STEUERN_EV_5 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_6](#job-steuern-ev-6) - 0x30D107FF STEUERN_EV_6 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_7](#job-steuern-ev-7) - 0x30D207FF STEUERN_EV_7 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_8](#job-steuern-ev-8) - 0x30D307FF STEUERN_EV_8 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_1_AUS](#job-steuern-ev-1-aus) - 0x30CB00 STEUERN_EV_1_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_2_AUS](#job-steuern-ev-2-aus) - 0x30CC00 STEUERN_EV_2_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_3_AUS](#job-steuern-ev-3-aus) - 0x30CD00 STEUERN_EV_3_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_4_AUS](#job-steuern-ev-4-aus) - 0x30CE00 STEUERN_EV_4_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_5_AUS](#job-steuern-ev-5-aus) - 0x30CF00 STEUERN_EV_5_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_6_AUS](#job-steuern-ev-6-aus) - 0x30D100 STEUERN_EV_6_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_7_AUS](#job-steuern-ev-7-aus) - 0x30D200 STEUERN_EV_7_AUS Stellgliedansteuerung Einspritzventile deaktivieren Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EV_8_AUS](#job-steuern-ev-8-aus) - 0x30D300 STEUERN_EV_8_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - 0x30C10700 STEUERN_E_LUEFTER Stellgliedansteuerung E-Luefter Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_E_LUEFTER_AUS](#job-steuern-e-luefter-aus) - 0x30C100 STEUERN_E_LUEFTER_AUS Stellgliedansteuerung E-Luefter Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_TEV](#job-start-systemcheck-tev) - 0x312200 START_SYSTEMCHECK_TEV Systemtest von TEV Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_TEV](#job-status-systemcheck-tev) - 0x2112 STATUS_SYSTEMCHECK_TEV Status Systemtest TEV Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_TEV](#job-stop-systemcheck-tev) - 0x322200 STOP_SYSTEMCHECK_TEV Beenden von TEV-Systemtest Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_TEV_AUS](#job-steuern-tev-aus) - 0x30C500 STEUERN_TEV_AUS Stellgliedansteuerung TEV vom Tester an DME freigeben Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_TEV](#job-steuern-tev) - 0x30C50704 STEUERN_TEV Stellgliedansteuerung TEV Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_KFK](#job-steuern-kfk) - 0x30C307FF STEUERN_KFK Stellgliedansteuerung KFK Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_KFK_AUS](#job-steuern-kfk-aus) - 0x30C300 STEUERN_KFK_AUS Stellgliedansteuerung KFK Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_MIL](#job-steuern-mil) - 0x30F107FF STEUERN_MIL Ansteuerung MIL (MIL blinken) Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_MIL_AUS](#job-steuern-mil-aus) - 0x30F100 STEUERN_MIL_AUS Beenden der MIL-Ansteuerung Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EML](#job-steuern-eml) - 0x30F307FF STEUERN_EML Stellgliedansteuerung EML Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EML_AUS](#job-steuern-eml-aus) - 0x30F300 STEUERN_EML_AUS Beenden der Stellgliedansteuerung EML Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EKP](#job-steuern-ekp) - 0xC607FF STEUERN_EKP Stellgliedansteuerung EKP Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EKP_AUS](#job-steuern-ekp-aus) - 0x30C600 STEUERN_EKP_AUS Stellgliedansteuerung EKP Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS1](#job-steuern-hls1) - 0x30C70705 STEUERN_HLS1 Stellgliedansteuerung Lambdasondenheizung 1 Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS1_AUS](#job-steuern-hls1-aus) - 0x30C700 STEUERN_HLS1_AUS Stellgliedansteuerung Lambdasondeheizung 1 aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS2](#job-steuern-hls2) - 0x30C80705 STEUERN_HLS2 Stellgliedansteuerung Lambdasondenheizung 2 Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS2_AUS](#job-steuern-hls2-aus) - 0x30C800 STEUERN_HLS2_AUS Stellgliedansteuerung Lambdasondeheizung 2 aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS3](#job-steuern-hls3) - 0x30C90705 STEUERN_HLS3 Stellgliedansteuerung Lambdasondenheizung 3 Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS3_AUS](#job-steuern-hls3-aus) - 0x30C900 STEUERN_HLS3_AUS Stellgliedansteuerung Lambdasondeheizung 3 aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS4](#job-steuern-hls4) - 0x30CA0705 STEUERN_HLS4 Stellgliedansteuerung Lambdasondenheizung 4 Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_HLS4_AUS](#job-steuern-hls4-aus) - 0x30CA00 STEUERN_HLS4_AUS Stellgliedansteuerung Lambdasondeheizung 4 aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EBL](#job-steuern-ebl) - 0x30D807FF STEUERN_EBL Stellgliedansteuerung E-Box-Luefter Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EBL_AUS](#job-steuern-ebl-aus) - 0x30D800 STEUERN_EBL_AUS Stellgliedansteuerung E-Box-Luefter aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_AGK](#job-steuern-agk) - 0x30D90700 STEUERN_AGK Stellgliedansteuerung Abgasklappe Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_AGK_AUS](#job-steuern-agk-aus) - 0x30D900 STEUERN_AGK_AUS Stellgliedansteuerung Abgasklappe aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DMTLP](#job-steuern-dmtlp) - 0x30DA07FF STEUERN_DMTLP Stellgliedansteuerung DM-TL Pumpe Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DMTLP_AUS](#job-steuern-dmtlp-aus) - 0x30DA00 STEUERN_DMTLP_AUS Stellgliedansteuerung DM-TL Pumpe aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DMTLV](#job-steuern-dmtlv) - 0x30DB07FF STEUERN_DMTLV Stellgliedansteuerung DM-TL Ventil Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DMTLV_AUS](#job-steuern-dmtlv-aus) - 0x30DB00 STEUERN_DMTLV_AUS Stellgliedansteuerung DM-TL Ventil aus Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DMTLH](#job-steuern-dmtlh) - 0x30F407FF STEUERN_DMTLH Ansteuerung DMTL-Heizung (nur bei US-Fahrzeugen) Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DMTLH_AUS](#job-steuern-dmtlh-aus) - 0x30F400 STEUERN_DMTLH_AUS Beenden Ansteuerung DMTL-Heizung Aktivierung: Klemme 15 = EIN Activation:
- [RAM_BACKUP](#job-ram-backup) - 0x31E900 RAM_BACKUP Loeschen der RAM-Backup-Werte Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_ZWANG_RAMBACKUP](#job-steuern-zwang-rambackup) - 0x31F200 STEUERN_ZWANG_RAMBACKUP Zwangssichern der RAM-Backup-Werte Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - 0x312600 START_SYSTEMCHECK_LLERH Diagnosefunktion LL-Erhoehung Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_LLERH](#job-status-systemcheck-llerh) - 0x2116 STATUS_SYSTEMCHECK_LLERH Diagnosefunktion LL-Erhoehung Status lesen Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - 0x322600 STOP_SYSTEMCHECK_LLERH Diagnosefunktion LL-Erhoehung Status lesen Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - 0x31DA00 START_SYSTEMCHECK_DMTL Start Systemtest DMTL Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_DMTL](#job-status-systemcheck-dmtl) - 0x2119 STATUS_SYSTEMCHECK_DMTL Status Systemtest DMTL Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - 0x32DA00 STOP_SYSTEMCHECK_DMTL Ende Systemtest DM-TL Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VANOS_EINLASS](#job-steuern-vanos-einlass) - 0x30E30700 STEUERN_VANOS_EINLASS Stellgliedansteuerung Einlass-VANOS Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VANOS_EINLASS_AUS](#job-steuern-vanos-einlass-aus) - 0x30E300 STEUERN_VANOS_EINLASS_AUS Stellgliedansteuerung Einlass-VANOS freigeben Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VANOS_AUSLASS](#job-steuern-vanos-auslass) - 0x30E40700 STEUERN_VANOS_AUSLASS Stellgliedansteuerung Auslass-VANOS Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VANOS_AUSLASS_AUS](#job-steuern-vanos-auslass-aus) - 0x30E400 STEUERN_VANOS_AUSLASS_AUS Stellgliedansteuerung Auslass-VANOS freigeben Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DISA](#job-steuern-disa) - 0x30E60700 STEUERN_DISA Stellgliedansteuerung DISA Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DISA_AUS](#job-steuern-disa-aus) - 0x30E600 STEUERN_DISA_AUS Stellgliedansteuerung DISA freigeben Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EVAUSBL](#job-steuern-evausbl) - 0x312500 STEUERN_EVAUSBL Systemdiagnose Einspritzventile ausblenden Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_EVAUSBL_AUS](#job-steuern-evausbl-aus) - 0x322500 STEUERN_EVAUSBL_AUS Ende Systemtest Einspritzventile ausblenden Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTE](#job-status-messwerte) - 0x224000 STATUS_MESSWERTE Auslesen von Messwerten Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTE_OEL](#job-status-messwerte-oel) - 0x224000 STATUS_MESSWERTE_OEL Auslesen von Oelwerten Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_BATTERIEINTEGRATOR](#job-status-batterieintegrator) - 0x224001 STATUS_BATTERIEINTEGRATOR Auslesen des Batterie-Ladezustands Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SCHALTERSTATI](#job-status-schalterstati) - 0x224002 STATUS_SCHALTERSTATI Auslesen von SchalterStatusflags Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FUNKTIONSSTATI](#job-status-funktionsstati) - 0x224007 STATUS_FUNKTIONSSTATI Auslesen der Funktionsstati Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_LAUFUNRUHE](#job-status-laufunruhe) - 0x224003 STATUS_LAUFUNRUHE Auslesen von Laufunruhewerten Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_DKHFM](#job-status-dkhfm) - 0x224008 STATUS_DKHFM Auslesen von DK/HFM-Abgleichswerten Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VVT](#job-steuern-vvt) - 0x30DD07 STEUERN_VVT VVT ansteuern Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VVT_AUS](#job-steuern-vvt-aus) - 0x30EE00 STEUERN_VVT_AUS beenden Stellgliedansteuerung VVT Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VVT_ENABLE](#job-steuern-vvt-enable) - 0x30E707FF STEUERN_VVT_ENABLE Generieren eines Testsignals auf der VVT-Enable-Leitung Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_VVT_ENABLE_AUS](#job-steuern-vvt-enable-aus) - 0x30E700 STEUERN_VVT_ENABLE_AUS Testsignal von VVT-Enable-Leitung zurücknehmen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_CO_ABGLEICH](#job-status-co-abgleich) - 0x30A201 STATUS_CO_ABGLEICH Auslesen des LL-CO-Wertes Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_CO_ABGLEICH_VERSTELLEN](#job-steuern-co-abgleich-verstellen) - 0x30A20700 STEUERN_CO_ABGLEICH_VERSTELLEN LL-CO-Wert vorgeben Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_CO_ABGLEICH_PROGRAMMIEREN](#job-steuern-co-abgleich-programmieren) - 0xA20800 STEUERN_CO_ABGLEICH_PROGRAMMIEREN LL-CO-WERT programmieren Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_GEMISCH](#job-status-gemisch) - 0x224004 STATUS_GEMISCH Auslesen von Gemischwerten Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_AUSGAENGE](#job-status-ausgaenge) - 0x224005 STATUS_AUSGAENGE Auslesen von Ausgaengen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_NOCKENWELLE_ADAPTION](#job-status-nockenwelle-adaption) - 0x224006 STATUS_NOCKENWELLE_ADAPTION Auslesen der NWG-Adaptionen Aktivierung: Klemme 15 = EIN Activation:
- [ECU_CONFIG](#job-ecu-config) - 0x30A801 ECU_CONFIG Auslesen der Variante Aktivierung: Klemme 15 = EIN Activation:
- [ECU_CONFIG_RESET](#job-ecu-config-reset) - 0x30A804 ECU_CONFIG_RESET Loeschen der Varianten Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_KVA](#job-status-kva) - 0x21C1 STATUS_KVA Auslesen Faktor KVA Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_KVA](#job-steuern-kva) - 0x3BC100 STEUERN_KVA Korrekturfaktor Kraftstoffverbrauch kva_korr programmieren Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_READINESS](#job-status-readiness) - 0x2105 STATUS_READINESS Auslesen des Readinessbyte Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FGR](#job-status-fgr) - 0x2107 STATUS_FGR Auslesen der FGR-Stati Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_LL_ABGLEICH](#job-steuern-ll-abgleich) - 0x30A107 STEUERN_LL_ABGLEICH Abgleichwert LL (Leerlauf) vorgeben Aktivierung: Klemme 15 = EIN UND Leerlauf = EIN Activation:
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - 0x30A108 STEUERN_LLABG_PROG Abgleichwert LL (Leerlauf) programmieren Aktivierung: Klemme 15 = EIN UND Leerlauf = EIN Activation:
- [STATUS_LL_ABGLEICH](#job-status-ll-abgleich) - 0x225FF0 STATUS_LL_ABGLEICH Abgleichwert LL (Leerlauf) auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_LRP](#job-status-lrp) - 0x30F601 STATUS_LRP Auslesen Funktionseingriffe bei der Laufruheprüfung Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_LRP](#job-steuern-lrp) - 0x30F607 STEUERN_LRP Funktionseingriffe für die Laufruheprüfung vorgeben Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_LRP_AUS](#job-steuern-lrp-aus) - 0x30F600 STEUERN_LRP_AUS Vorgabe Funktionseingriffe für die Laufruheprüfung stoppen Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_PROGRAMM_LRP](#job-steuern-programm-lrp) - 0x30F608 STEUERN_PROGRAMM_LRP Prüfeingriffe für die Laufruheprüfung programmieren Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTE_LRP](#job-status-messwerte-lrp) - 0x22402D STATUS_MESSWERTE_LRP Ausgelesen der Messwerte Laufruheprüfung Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTE_VVT](#job-status-messwerte-vvt) - 0x22400B STATUS_MESSWERTE_VVT VVT Messwerte auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA1](#job-status-fasta1) - 0x22400C STATUS_FASTA1 Auslesen FASTA-Messwertblock 1 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA2](#job-status-fasta2) - 0x22400D STATUS_FASTA2 Auslesen FASTA-Messwertblock 2 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA3](#job-status-fasta3) - 0x22400E STATUS_FASTA3 Auslesen FASTA-Messwertblock 3 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA4](#job-status-fasta4) - 0x22400F STATUS_FASTA4 Auslesen FASTA-Messwertblock 4 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA5](#job-status-fasta5) - 0x224010 STATUS_FASTA5 Auslesen FASTA-Messwertblock 5 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA6](#job-status-fasta6) - 0x224011 STATUS_FASTA6 Auslesen FASTA-Messwertblock 6 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA7](#job-status-fasta7) - 0x224012 STATUS_FASTA7 Auslesen FASTA-Messwertblock 7 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_FASTA10](#job-status-fasta10) - 0x224015 STATUS_FASTA10 Auslesen FASTA-Messwertblock 10 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTBLOCK_ADC](#job-status-messwertblock-adc) - 0x304101 STATUS_MESSWERTBLOCK_ADC Auslesen ADC-Werte Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_LSU](#job-start-systemcheck-lsu) - 0x31E800 START_SYSTEMCHECK_LSU Systemdiagnose LSU starten Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_LSU](#job-status-systemcheck-lsu) - 0x2125 STATUS_SYSTEMCHECK_LSU Status Systemdiagnose LSU Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_LSU_NEU](#job-status-systemcheck-lsu-neu) - 0x2125 STATUS_SYSTEMCHECK_LSU_NEU Status Systemdiagnose LSU Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_LSU](#job-stop-systemcheck-lsu) - 0x32E800 STOP_SYSTEMCHECK_LSU Ende Systemdiagnose LSU Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_KAT](#job-start-systemcheck-kat) - 0x31EB00 START_SYSTEMCHECK_KAT Systemdiagnose KAT Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_KAT](#job-status-systemcheck-kat) - 0x211C STATUS_SYSTEMCHECK_KAT Status Systemtest KAT Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_KAT](#job-stop-systemcheck-kat) - 0x32EB00 STOP_SYSTEMCHECK_KAT Ende Systemdiagnose KAT Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_DIAGNOSE_LSV](#job-status-diagnose-lsv) - 0x31402C45 und 0x31402C46 STATUS_DIAGNOSE_LSV Status LSV-Diagnose auslesen Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_LSH](#job-start-systemcheck-lsh) - 0x31ED00 START_SYSTEMCHECK_LSH Start der Systemdiagnose LSH Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_LSH](#job-status-systemcheck-lsh) - 0x31402C71 und 0x31402C72 STATUS_SYSTEMCHECK_LSH Status LSH-Diagnose auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_LSH](#job-stop-systemcheck-lsh) - 0x32ED00 STOP_SYSTEMCHECK_LSH Ende der Systemdiagnose LSH Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_GRUNDADAPT](#job-start-systemcheck-grundadapt) - 0x313200 START_SYSTEMCHECK_GRUNDADAPT Systemdiagnose Grundadaptionenen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_GRUNDADAPT](#job-status-systemcheck-grundadapt) - 0x2127 STATUS_SYSTEMCHECK_GRUNDADAPT Status Systemdiagnose Grundadaptionen starten Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_GRUNDADAPT](#job-stop-systemcheck-grundadapt) - 0x323200 STOP_SYSTEMCHECK_GRUNDADAPT Ende Systemdiagnose Grundadaptionen starten Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_GEMISCHADAPT_SPERR](#job-start-systemcheck-gemischadapt-sperr) - 0x31D800 START_SYSTEMCHECK_GEMISCHADAPT_SPERR Systemdiagnose Gemischadaptionen sperren Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR](#job-stop-systemcheck-gemischadapt-sperr) - 0x32D800 STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR Ende Systemdiagnose Gemischadaptionen sperren Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_LAMBDA_AUS](#job-start-systemcheck-lambda-aus) - 0x31D900 START_SYSTEMCHECK_LAMBDA_AUS Systemdiagnose Labdaregelung aus Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_LAMBDA_AUS](#job-status-systemcheck-lambda-aus) - 0x2118 STATUS_SYSTEMCHECK_LAMBDA_AUS Status Systemdiagnose Lambdaregelung aus Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_LAMBDA_AUS](#job-stop-systemcheck-lambda-aus) - 0x32D900 STOP_SYSTEMCHECK_LAMBDA_AUS Ende Systemdiagnose Lambdaregelung aus Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_KOMPRESSION](#job-start-systemcheck-kompression) - 0x31F300 START_SYSTEMCHECK_KOMPRESSION Systemdiagnose Kompressionstest Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_KOMPRESSION](#job-stop-systemcheck-kompression) - 0x32F300 STOP_SYSTEMCHECK_KOMPRESSION Ende Systemdiagnose Kompressiostest Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_RUHESTROMMESSUNG](#job-steuern-ruhestrommessung) - 0x312B STEUERN_RUHESTROMMESSUNG Ansteuern Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_RUHESTROMMESSUNG](#job-status-ruhestrommessung) - 0x332B STATUS_RUHESTROMMESSUNG Auslesen Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation:
- [START_SYSTEMCHECK_GLF](#job-start-systemcheck-glf) - 0x31D5 START_SYSTEMCHECK_GLF Start Systemcheck 'geführte Luftsteuerung' Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_GLF](#job-stop-systemcheck-glf) - 0x32D5 STOP_SYSTEMCHECK_GLF Systemcheck 'geführte Luftsteuerung' beenden Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_GLF](#job-status-systemcheck-glf) - 0x33D5 STATUS_SYSTEMCHECK_GLF Stati Systemcheck 'geführte Luftsteuerung' Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_GLF](#job-steuern-glf) - 0x30ED07FF000A STEUERN_GLF Stellgliedansteuerung GLF (obere Klappe) Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_ENDE_GLF](#job-steuern-ende-glf) - 0x30ED00 STEUERN_ENDE_GLF Ansteuerung GLF (obere Klappe) beenden Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_GLF](#job-status-glf) - 0x30ED01 STATUS_GLF Status obere und untere Klappe Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_GLF2](#job-steuern-glf2) - 0x30BE07FF000A STEUERN_GLF2 Stellgliedansteuerung GLF2 (untere Klappe) Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_ENDE_GLF2](#job-steuern-ende-glf2) - 0x30BE00 STEUERN_ENDE_GLF2 Stellgliedansteuerung GLF beenden Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_GLF2](#job-status-glf2) - 0x30BE01 STATUS_GLF2 Status obere und untere Klappe Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_DISA_ANSCHLAG](#job-steuern-disa-anschlag) - 0x31E600 STEUERN_DISA_ANSCHLAG lernen der DISA-Anschlaege Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_DISA_ANSCHLAG](#job-status-disa-anschlag) - 0x212A STATUS_DISA_ANSCHLAG Status Lernen der DISA-Anschlaege Aktivierung: Klemme 15 = EIN Activation:
- [STOP_DISA_ANSCHLAG](#job-stop-disa-anschlag) - 0x32E600 STOP_DISA_ANSCHLAG Ende des Lernes DISA-Anschlaege Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MINHUB](#job-status-minhub) - 0x30A301 STATUS_MINHUB Auslesen VVT-Minhub Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_MINHUB](#job-steuern-minhub) - 0x22400F STEUERN_MINHUB VVT-Minhub vorgeben Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_MINHUB_PROGRAMM](#job-steuern-minhub-programm) - 0x30A308010000 STEUERN_MINHUB_PROGRAMM Programmieren VVT-Minhub Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_BANKABGLEICH](#job-status-bankabgleich) - 0x30A401 STATUS_BANKABGLEICH Auslesen des VVT-Bankabgleiches Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_BANKABGLEICH_PROGRAMM](#job-steuern-bankabgleich-programm) - 0x30A408010000 STEUERN_BANKABGLEICH_PROGRAMM Programmieren des Winkeloffset Excenterwelle (ofwnktest) Verstellbereich Bank 1: 0°...5° Verstellbereich Bank 2: 0°...-5° Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - 0x21C3 STATUS_BETRIEBSSTUNDENZAEHLER Status Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation:
- [DME_STARTWERT_ABGLEICH](#job-dme-startwert-abgleich) - Kopiert die ISN auf beide Wechselcodes KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $20 Modus  : Default
- [EWS_STARTWERT](#job-ews-startwert) - 0x318300 EWS_STARTWERT EWS-Startwertinitialisierung Aktivierung: Klemme 15 = EIN Activation:
- [EWS_EMPFANG](#job-ews-empfang) - 0x2106 EWS_EMPFANG EWS-Empfangsstatus auslesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - 0x224000 STATUS_MOTORTEMPERATUR Auslesen der Motortemperatur Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - 0x224000 STATUS_MOTORDREHZAHL Auslesen der Motordrehzahl Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - 0x224000 STATUS_AN_LUFTTEMPERATUR Auslesen der Lufttemperatur Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - 0x224000 STATUS_LMM_MASSE Auslesen der Luftmasse Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_L_SONDE](#job-status-l-sonde) - 0x224003 STATUS_L_SONDE Auslesen der Lambdasondenspannung vorne Bank 1 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - 0x224003 STATUS_L_SONDE_2 Auslesen der Lambdasondenspannung vorne Bank 2 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_L_SONDE_H](#job-status-l-sonde-h) - 0x304801 STATUS_L_SONDE_H Auslesen der Lambdasondenspannung hinten Bank 1 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_L_SONDE_2_H](#job-status-l-sonde-2-h) - 0x304501 STATUS_L_SONDE_2_H Auslesen der Lambdasondenspannung hinten Bank 2 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_INT](#job-status-int) - 0x224000 STATUS_INT Auslesen der Lambdaregelung Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_INT_2](#job-status-int-2) - 0x224000 STATUS_INT_2 Auslesen der Lambdaregelung Bank 2 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_ADD](#job-status-add) - 0x224004 STATUS_ADD Auslesen der additiven Lambdaregelung Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_ADD_2](#job-status-add-2) - 0x224004 STATUS_ADD_2 Auslesen der additiven Lambdaregelung Bank 2 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MUL](#job-status-mul) - 0x224004 STATUS_MUL Auslesen der multipikativen Lambdaregelung Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MUL_2](#job-status-mul-2) - 0x224004 STATUS_MUL_2 Auslesen der multipikativen Lambdaregelung Bank 2 Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MOTORLAUFUNRUHE](#job-status-motorlaufunruhe) - 0x224003 STATUS_MOTORLAUFUNRUHE Auslesen der Laufunruhewerte Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_UBATT](#job-status-ubatt) - 0x224000 STATUS_UBATT Auslesen der Batteriespannung Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - 0x224006 STATUS_GEBERRAD_ADAPTION Auslesen der NWG-Adaptionen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_DIGITAL](#job-status-digital) - 0x224002 & 0x224007 STATUS_DIGITAL Auslesen der Schalter- und Funktionsstati Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - 0x304601 & 0x304701 STATUS_PWG_POTI_SPANNUNG Auslesen des Pedalwertgebers Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTE_IBS](#job-status-messwerte-ibs) - 0x22402B STATUS_MESSWERTE_IBS Auslesen von Temperatur, Spannung und Strom der Batterie Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTE_GEN](#job-status-messwerte-gen) - 0x22402C STATUS_MESSWERTE_GEN Auslesen der Generator-Messwerte Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_MESSWERTE_VAD](#job-status-messwerte-vad) - 0x224025 STATUS_MESSWERTE_VAD Variantenadaptionen auslesen Aktivierung: Klemme 15 = EIN Activation:
- [IDENT_IBS](#job-ident-ibs) - 0x224021 IDENT_IBS Identifikationsdaten für IBS auslesen (BMW Nr, Seriennummer, SW/HW Index) Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_PM_INFO_1](#job-status-systemcheck-pm-info-1) - 0x224022 STATUS_SYSTEMCHECK_PM_INFO_1 Batterie Powermanagement Bytefeld 1 lesen Aktivierung: Klemme 15 = EIN Activation:
- [STATUS_SYSTEMCHECK_PM_INFO_2](#job-status-systemcheck-pm-info-2) - 0x224023 STATUS_SYSTEMCHECK_PM_INFO_2 Batterie Powermanagement Bytefeld 2 lesen Aktivierung: Klemme 15 = EIN Activation:
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - 0x2E5FF504 STEUERN_PM_HISTOGRAM_RESET Löschen der Powermanagement-Infofelder Aktivierung: Klemme 15 = EIN Activation:
- [ADAP_SELEKTIV_LOESCHEN](#job-adap-selektiv-loeschen) - 0x3130 ADAP_SELEKTIV_LOESCHEN Löschen von Adaptionen und gelernte Varianten Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation:
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - 0x3130001000 STEUERN_BATTERIETAUSCH_REGISTRIEREN Batterietausch registrieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation:
- [START_SYSTEMCHECK_PM_MESSEMODE](#job-start-systemcheck-pm-messemode) - 0x31F6 START_SYSTEMCHECK_PM_MESSEMODE Systemdiagnose BatterieSensor Messemode setzen Aktivierung: Klemme 15 = EIN Activation:
- [STOP_SYSTEMCHECK_PM_MESSEMODE](#job-stop-systemcheck-pm-messemode) - 0x32F6 STOP_SYSTEMCHECK_PM_MESSEMODE Systemdiagnose BatterieSensor Messmode beenden Aktivierung: Klemme 15 = EIN Activation:
- [_STATUS_IGRINFO](#job-status-igrinfo) - 0x224016 _STATUS_IGRINFO Infospeicher Intelligente Generator Regelung (IGR) auslesen Aktivierung: Klemme 15 = EIN Activation:
- [_STATUS_LEMINFO](#job-status-leminfo) - 0x224017 _STATUS_LEMINFO Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen Aktivierung: Klemme 15 = EIN Activation:

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

<a id="job-cbs-info"></a>
### CBS_INFO

Ausgabe der CBS-Version

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ECU_NAME | string | Steuergeraetename |
| CBS_VERSION_TEXT | string | CBS Version im Klartext |
| CBS_VERSION_HEX | string | CBS Version als Wert |

<a id="job-cbs-daten-lesen"></a>
### CBS_DATEN_LESEN

CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Hex-String |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergeraet |
| ID_FN_CBS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_CBS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_CBS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_CBS_WERT | int | Restlaufleistung |
| RMMI_CBS_EINH | string | Information zur Restlaufleistung |
| ST_UN_CBS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_CBS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_CBS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_CBS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_CBS_MESS_EINH | string | Zaehler |
| AVAI_CBS_WERT | int | Verfuegbarkeit in % |
| AVAI_CBS_EINH | string | % |
| AVAI_CBS_WERT_OEL | int | Verfuegbarkeit OEL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_CSF | int | Verfuegbarkeit CSF in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BATT | int | Verfügbarkeit BATT in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_VTG | int | Verfügbarkeit VTG in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_FILT | int | Verfuegbarkeit FILT in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_V | int | Verfuegbarkeit BR_V in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_H | int | Verfuegbarkeit BR_H in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BRFL | int | Verfuegbarkeit BRFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ | int | Verfuegbarkeit ZKRZ in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC | int | Verfuegbarkeit SIC in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_KFL | int | Verfuegbarkeit KFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_UEB | int | Verfuegbarkeit UEB in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_DAD | int | Verfuegbarkeit DAD in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ_A | int | Verfuegbarkeit ZKRZ_A in %, fuer Pruefablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr |
| ZIEL_YY_EINH | string | Jahr |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall |
| FRC_INTM_WAY_CBS_EINH | string | Information zur Prognose Wegintervall |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall |
| MANIP_CBS | int | Manipulationsbyte |
| MANIP_CBS_TEXT | string | Manipulationsbyte im Klartext |
| Res_Byte | int | Reserve Byte (noch unbenutzt) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG, ZKrz_a, DAD Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 255 Defaultwert: 100 |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| RMM_CBS_WERT | int | Restlaufleistung in km oder % (siehe Argument Einheit) Schalter, keine Aenderung: 8000h Defaultwert: 8000h |
| ST_UN_CBS_RSTG | int | Einheit Restlaufleistung 0hex -&gt; % 1hex -&gt; km*10 Fhex -&gt; d.c. Defaultwert: Fh |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall Umrechnung 1-254*1000km Schalter, setzt auf Defaultwert zurueck: 0h Schalter, keine Aenderung: FFh Defaultwert: FFh |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall 0-254 Monate Schalter, keine Aenderung: FFh Defaultwert: FFh |
| Res_Byte | int | Reserve Byte (noch unbenutzt) Defaultwert: 00h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
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

<a id="job-status-bzeinfo"></a>
### _STATUS_BZEINFO

0x22401A _STATUS_BZEINFO Infospeicher Batterie Zustands Erkennung (BZE) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QV_OUT_M_WERT | real | Gueltiger gemittelter Kapazitaetsverlust (A2L-Name: Qv_out_m) Qv_out_m   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_OUT_M_EINH | string | percent |
| STAT_QV_QUALI_M_WERT | real | Qualitaetsindex fuer gemittelten Qv-Wert (A2L-Name: Qv_quali_m) Qv_quali_m   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_M_EINH | string | percent |
| STAT_QV_STATUS | long | Prozessstatus / Trend fuer gemittelten Qv-Wert (A2L-Name: Qv_status) Qv_status   Min: -128 Max: 127 |
| STAT_QV_OUT_1_WERT | long | Kapazitaetsverlust letzter Start (A2L-Name: Qv_out_1) Qv_out_1   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_1_EINH | string | Ah |
| STAT_QV_OUT_2_WERT | long | Kapazitaetsverlust 2. letzter Start (A2L-Name: Qv_out_2) Qv_out_2   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_2_EINH | string | Ah |
| STAT_QV_OUT_3_WERT | long | Kapazitaetsverlust 3. letzter Start (A2L-Name: Qv_out_3) Qv_out_3   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_3_EINH | string | Ah |
| STAT_QV_OUT_4_WERT | long | Kapazitaetsverlust 4. letzter Start (A2L-Name: Qv_out_4) Qv_out_4   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_4_EINH | string | Ah |
| STAT_QV_OUT_5_WERT | long | Kapazitaetsverlust 5. letzter Start (A2L-Name: Qv_out_5) Qv_out_5   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_5_EINH | string | Ah |
| STAT_QV_QUALI_1_WERT | real | Qualitaetsindex letzter Qv-Wert (A2L-Name: Qv_quali_1) Qv_quali_1   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_1_EINH | string | percent |
| STAT_QV_QUALI_2_WERT | real | Qualitaetsindex 2. letzter Qv-Wert (A2L-Name: Qv_quali_2) Qv_quali_2   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_2_EINH | string | percent |
| STAT_QV_QUALI_3_WERT | real | Qualitaetsindex 3. letzter Qv-Wert (A2L-Name: Qv_quali_3) Qv_quali_3   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_3_EINH | string | percent |
| STAT_QV_QUALI_4_WERT | real | Qualitaetsindex 4. letzter Qv-Wert (A2L-Name: Qv_quali_4) Qv_quali_4   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_4_EINH | string | percent |
| STAT_QV_QUALI_5_WERT | real | Qualitaetsindex 5. letzter Qv-Wert (A2L-Name: Qv_quali_5) Qv_quali_5   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_5_EINH | string | percent |
| STAT_QV_TD1_WERT | unsigned long | Zeit seit Qv_out_1 Berechnung (A2L-Name: Qv_td1) Qv_td1   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD1_EINH | string | h |
| STAT_QV_TD2_WERT | unsigned long | Zeit zwischen Qv_out_1 und Qv_out_2 (A2L-Name: Qv_td2) Qv_td2   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD2_EINH | string | h |
| STAT_QV_TD3_WERT | unsigned long | Zeit zwischen Qv_out_2 und Qv_out_3 (A2L-Name: Qv_td3) Qv_td3   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD3_EINH | string | h |
| STAT_QV_TD4_WERT | unsigned long | Zeit zwischen Qv_out_3 und Qv_out_4 (A2L-Name: Qv_td4) Qv_td4   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD4_EINH | string | h |
| STAT_QV_TD5_WERT | unsigned long | Zeit zwischen Qv_out_4 und Qv_out_5 (A2L-Name: Qv_td5) Qv_td5   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD5_EINH | string | h |
| STAT_QVC_STATUS_1_WERT | real | Ausgang fÃ¼r SchluesselgroeÃŸe 1 (A2L-Name: Qvc_status_1) Qvc_status_1   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QVC_STATUS_1_EINH | string | percent |
| STAT_QVC_STATUS_2_WERT | real | Ausgang fÃ¼r SchluesselgroeÃŸe 2 (A2L-Name: Qvc_status_2) Qvc_status_2   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QVC_STATUS_2_EINH | string | percent |
| STAT_QVC_STATUS_3 | unsigned long | Ausgang fÃ¼r SchluesselgroeÃŸe 3 (A2L-Name: Qvc_status_3) Qvc_status_3   Min: 0 Max: 255 |
| STAT_QVC_STATUS_4 | long | Ausgang fÃ¼r SchluesselgroeÃŸe 4 (A2L-Name: Qvc_status_4) Qvc_status_4   Min: -128 Max: 127 |
| STAT_QV_NV_ZH | unsigned long | Anzahl der Hystereseauswertungen (A2L-Name: Qv_nv_zh) Qv_nv_zh   Min: 0 Max: 4294967295 |
| STAT_QV_NV_EZM_WERT | real | Mittlerer Fehler fuer gesamte Hystereseberechnung (A2L-Name: Qv_nv_ezm) Qv_nv_ezm   Min: 0 Max: 1 |
| STAT_QV_H2O_WERT | real | Bisheriger Wasserverlust Batterie (A2L-Name: Qv_h2o) Qv_h2o   Min: 0 Max: 63.999 |
| STAT_QV_H2OQUALI_WERT | real | Qualitaetswert fuer Wasserverlust Batterie (A2L-Name: Qv_h2oquali) Qv_h2oquali   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_H2OQUALI_EINH | string | percent |
| STAT_ST_QVC1 | unsigned long | Statuswort (A2L-Name: St_qvc1) Bedeutung: - 0: Wasserverlust O.K. - 1: Wasserverlust zu hoch St_qvc1   Min: 0 Max: 255 |
| STAT_QV_H2OSTATUS | unsigned long | Status fuer Entwicklung Wasserverlust (A2L-Name: Qv_h2ostatus) Qv_h2ostatus   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geninfo"></a>
### _STATUS_GENINFO

0x22401B _STATUS_GENINFO Infospeicher Generatordiagnose erweitert auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DGENUB1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENUB1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_EINH | string | V |
| STAT_DGENUB2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENUB2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_EINH | string | V |
| STAT_DGENUBNZ_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENUBNZ   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_EINH | string | V |
| STAT_DGENUBERR1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENUBERR2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENUBERRNZ | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENUGEN1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENUGEN1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_EINH | string | V |
| STAT_DGENUGEN2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENUGEN2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN2_EINH | string | V |
| STAT_DGENUGENNZ_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENUGENNZ   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_EINH | string | V |
| STAT_DGENUGENERR1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENUGENERR2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENGRENZ1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENGRENZ1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_EINH | string | A |
| STAT_DGENGRENZ2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENGRENZ2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_EINH | string | A |
| STAT_DGENGRENZNZ_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENGRENZNZ   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_EINH | string | A |
| STAT_DGENGRENZERR1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENGRENZERR2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENUB1_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENUB1_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_MD1_EINH | string | V |
| STAT_DGENUB2_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENUB2_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_MD1_EINH | string | V |
| STAT_DGENUBNZ_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENUBNZ_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_MD1_EINH | string | V |
| STAT_DGENUBERR1_MD1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERR2_MD1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERRNZ_MD1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGEN1_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENUGEN1_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_MD1_EINH | string | V |
| STAT_DGENUGEN2_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENUGEN2_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN2_MD1_EINH | string | V |
| STAT_DGENUGENNZ_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENUGENNZ_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_MD1_EINH | string | V |
| STAT_DGENUGENERR1_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERR2_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZ1_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENGRENZ1_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_MD1_EINH | string | A |
| STAT_DGENGRENZ2_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENGRENZ2_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_MD1_EINH | string | A |
| STAT_DGENGRENZNZ_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENGRENZNZ_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_MD1_EINH | string | A |
| STAT_DGENGRENZERR1_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERR2_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUB1_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENUB1_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_MD2_EINH | string | V |
| STAT_DGENUB2_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENUB2_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_MD2_EINH | string | V |
| STAT_DGENUBNZ_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENUBNZ_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_MD2_EINH | string | V |
| STAT_DGENUBERR1_MD2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERR2_MD2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERRNZ_MD2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGEN1_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENUGEN1_MD2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_MD2_EINH | string | V |
| STAT_DGENUGEN2_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENUGEN2_MD2   Einheit: V   Min: 0 Max: 25.5 |
| STAT_DGENUGEN2_MD2_EINH | string | V |
| STAT_DGENUGENNZ_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENUGENNZ_MD2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_MD2_EINH | string | V |
| STAT_DGENUGENERR1_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERR2_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZ1_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENGRENZ1_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_MD2_EINH | string | A |
| STAT_DGENGRENZ2_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENGRENZ2_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_MD2_EINH | string | A |
| STAT_DGENGRENZNZ_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENGRENZNZ_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_MD2_EINH | string | A |
| STAT_DGENGRENZERR1_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERR2_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMRUHVERL_MD1 | unsigned long | PM Ruhestromverletzung zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBATT_MD1 | unsigned long | Fehler PM Batterie zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBN_MD1 | unsigned long | Fehler PM Bordnetz zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSDGLOB_MD1 | unsigned long | Fehler BSD global zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_4_MD1 | unsigned long | Kommunikation QLT zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_3_MD1 | unsigned long | Kommunikation EWAPU zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_0_MD1 | unsigned long | Kommunikation IBS zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENREGUPL_MD1 | unsigned long | Generatorfehler Reglertyp unplausibel zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHTB_MD1 | unsigned long | Generatorfehler Hochtemperatur berechnet zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENELB_MD1 | unsigned long | Generatorfehler elektrisch berechnet zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENKOMM_MD1 | unsigned long | Kommunikation Generator zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENUPL_MD1 | unsigned long | Generatorfehler Typ unplausibel zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHT_MD1 | unsigned long | Generatorfehler Hochtemperatur (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENMECH_MD1 | unsigned long | Generatorfehler mechanisch (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENEL_MD1 | unsigned long | Generatorfehler elektrisch (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMRUHVERL_MD2 | unsigned long | PM Ruhestromverletzung zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBATT_MD2 | unsigned long | Fehler PM Batterie zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBN_MD2 | unsigned long | Fehler PM Bordnetz zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSDGLOB_MD2 | unsigned long | Fehler BSD global zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_4_MD2 | unsigned long | Kommunikation QLT zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_3_MD2 | unsigned long | Kommunikation EWAPU zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_0_MD2 | unsigned long | Kommunikation IBS zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENREGUPL_MD2 | unsigned long | Generatorfehler Reglertyp unplausibel zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHTB_MD2 | unsigned long | Generatorfehler Hochtemperatur berechnet zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENELB_MD2 | unsigned long | Generatorfehler elektrisch berechnet zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENKOMM_MD2 | unsigned long | Kommunikation Generator zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENUPL_MD2 | unsigned long | Generatorfehler Typ unplausibel zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHT_MD2 | unsigned long | Generatorfehler Hochtemperatur (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENMECH_MD2 | unsigned long | Generatorfehler mechanisch (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENEL_MD2 | unsigned long | Generatorfehler elektrisch (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-data-id-lesen"></a>
### DATA_ID_LESEN

0x222504 DATA_ID_LESEN Data-ID des SG auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATA_ID | string | ASCII-String fuer Data-ID |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-progstand-long-lesen"></a>
### PROGSTAND_LONG_LESEN

0x222504 PROGSTAND_LONG_LESEN Programmstand-Nr. des SG auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| PROGSTAND_LONG | long |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-aif"></a>
### IDENT_AIF

0x1A80 und 0x23 IDENT_AIF Identdaten und Anwender Informations Felder Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
| ID_LIEF_TEXT | string | Lieferanten-Text nach Tabelle Lieferanten |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| AIF_ADRESSE | long | AIF Adresse |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_PROGRAMMIER_DATUM | string | Datum der SG-Programmierung in der Form JJJJ.MM.TT |
| AIF_ZUSAMMENBAU_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_DATENSATZ_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_TESTER_NR | string | Tester Seriennummer |
| AIF_KM_STAND | long | km-Stand bei der Programmierung |
| AIF_PROGRAMM_STAND | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-power-down"></a>
### STEUERN_POWER_DOWN

Anforderung Power Down Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-bze"></a>
### STATUS_CODIERUNG_BZE

0x223230 STATUS_CODIERUNG_BZE Codierung fuer BZE (Batterie Zustands Erkennung) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CD_HERST1 | unsigned long | Codierung Hersteller 1 (A2L-Name: Qv_cdherst_2) Qv_cdherst_1   Min: 0 Max: 255 |
| STAT_CD_HERST2 | unsigned long | Codierung Hersteller 2 (A2L-Name: Qv_cdherst_2) Qv_cdherst_2   Min: 0 Max: 255 |
| STAT_CD_HERST3 | unsigned long | Codierung Hersteller 3 (A2L-Name: Qv_cdherst_3) Qv_cdherst_3   Min: 0 Max: 255 |
| STAT_CD_HERST4 | unsigned long | Codierung Hersteller 4 (A2L-Name: Qv_cdherst_4) Qv_cdherst_4   Min: 0 Max: 255 |
| STAT_CD_HERST5 | unsigned long | Codierung Hersteller 5 (A2L-Name: Qv_cdherst_5) Qv_cdherst_5   Min: 0 Max: 255 |
| STAT_CD_HERST6 | unsigned long | Codierung Hersteller 6 (A2L-Name: Qv_cdherst_6) Qv_cdherst_6   Min: 0 Max: 255 |
| STAT_CD_HERST7 | unsigned long | Codierung Hersteller 7 (A2L-Name: Qv_cdherst_7) Qv_cdherst_7   Min: 0 Max: 255 |
| STAT_CD_HERST8 | unsigned long | Codierung Hersteller 8 (A2L-Name: Qv_cdherst_8) Qv_cdherst_8   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-igr"></a>
### STATUS_CODIERUNG_IGR

0x223210 STATUS_CODIERUNG_IGR Codierung fuer IGR (Intelligente Generator-Regelung) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_IGR_TEXT | string | Codierung IGR auslesen B_CDIGRONR   Min: 0 Max: 1 |
| STAT_CODIERUNG_IGR_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-kat"></a>
### STATUS_CODIERUNG_KAT

0x223001 STATUS_CODIERUNG_KAT Codierung fuer Katalysator auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_KAT | unsigned long | Status fuer Codierung Katalysator CWKATVAR |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-mil"></a>
### STATUS_CODIERUNG_MIL

0x223000 STATUS_CODIERUNG_MIL Codierung fuer MIL (Malfunction Indication Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_MIL | unsigned long | Status fuer Codierung MIL CWNOMILCOD |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-oel"></a>
### STATUS_CODIERUNG_OEL

0x223200 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERFAKTOR_1_WERT | real | Status fuer Codierung Laenderfaktor 1 OZLF_1 |
| STAT_LAENDERFAKTOR_2_WERT | real | Status fuer Codierung Laenderfaktor 2 OZLF_2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-protokoll"></a>
### STATUS_CODIERUNG_PROTOKOLL

0x223030 STATUS_CODIERUNG_PROTOKOLL Codierung Protokoll auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PROTOKOLL | unsigned long | Ausgabe Codierung Protokoll: 0 = Protokoll 15765_4 Anlieferzustand  1 = Protokoll 15765_4 codiert  2 = Protokoll 14230 codiert CWISOCAN |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-spa"></a>
### STATUS_CODIERUNG_SPA

0x223220 STATUS_CODIERUNG_SPA Codierung fuer SPA (Schaltpunktanzeige) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_B_SPA_CSOLL_TEXT | string | Codierung Schaltpunktanzeige (SPA), 0 = Auslieferungszustand, 1 = Abweichung zum Auslieferungszustand B_SPA_CSOLL   Min: 0 Max: 1 |
| STAT_B_SPA_CSOLL_WERT | int |  |
| STAT_B_SPA_CIST_TEXT | string | ZurÃ¼ckgemeltdete Codierung SPA, 0 = Schaltpunktanzeige inaktiv, 1 = Schaltpunktanzeige aktiv B_SPA_CIST   Min: 0 Max: 1 |
| STAT_B_SPA_CIST_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-vmax"></a>
### STATUS_CODIERUNG_VMAX

0x223010 STATUS_CODIERUNG_VMAX Codierung fuer maximale Geschwindigkeit auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_VMAX | unsigned long | Status fuer Codierung maximale Geschwindigkeit CWVMAXCOD |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-xenon"></a>
### STATUS_CODIERUNG_XENON

0x223211 STATUS_CODIERUNG_XENON Codierung fuer Xenon-Lichtverbau auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_XENON_TEXT | string | Codierung Xenonverbau auslesen B_CDXENONR |
| STAT_CODIERUNG_XENON_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmmode9"></a>
### STATUS_RBMMODE9

0x224026 STATUS_RBMMODE9 Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_M9GENDEN_WERT | unsigned long | Wert von m9genden_w |
| STAT_M9IGNCYC_WERT | unsigned long | Wert von m9igncyc_w |
| STAT_M9NMCAT1_WERT | unsigned long | Wert von m9nmcat1_w |
| STAT_M9DNCAT1_WERT | unsigned long | Wert von m9dncat1_w |
| STAT_M9NMCAT2_WERT | unsigned long | Wert von m9nmcat2_w |
| STAT_M9DNCAT2_WERT | unsigned long | Wert von m9dncat2_w |
| STAT_M9NMOXS1_WERT | unsigned long | Wert von m9nmoxs1_w |
| STAT_M9DNOXS1_WERT | unsigned long | Wert von m9dnoxs1_w |
| STAT_M9NMOXS2_WERT | unsigned long | Wert von m9nmoxs2_w |
| STAT_M9DNOXS2_WERT | unsigned long | Wert von m9dnoxs2_w |
| STAT_M9NMEGR_WERT | unsigned long | Wert von m9nmegr_w |
| STAT_M9DNEGR_WERT | unsigned long | Wert von m9dnegr_w |
| STAT_M9NMSAIR_WERT | unsigned long | Wert von m9nmsair_w |
| STAT_M9DNSAIR_WERT | unsigned long | Wert von m9dnsair_w |
| STAT_M9NMEVAP_WERT | unsigned long | Wert von m9nmevap_w |
| STAT_M9DNEVAP_WERT | unsigned long | Wert von m9dnevap_w |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmme1"></a>
### STATUS_RBMME1

0x224029 STATUS_RBMME1 Lesen der RBM-Werte Block1 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUMERATOR_KATSP | unsigned long | Numerator Katalysator Bank 1 |
| STAT_DENOMINATOR_KATSP | unsigned long | Denominator Katalysator Bank 1 |
| STAT_NUMERATOR_KATSP2 | unsigned long | Numerator Katalysator Bank 2 |
| STAT_DENOMINATOR_KATSP2 | unsigned long | Denominator Katalysator Bank 2 |
| STAT_NUMERATOR_DYLSU | unsigned long | Numerator LSU dynamisch zu langsam Bank 1 |
| STAT_DENOMINATOR_DYLSU | unsigned long | Denominator LSU dynamisch zu langsam Bank 1 |
| STAT_NUMERATOR_DYLSU2 | unsigned long | Numerator LSU dynamisch zu langsam Bank 2 |
| STAT_DENOMINATOR_DYLSU2 | unsigned long | Denominator LSU dynamisch zu langsam Bank 2 |
| STAT_NUMERATOR_ULSU | unsigned long | Numerator Spannungsüberwachung LSU Bank 1 |
| STAT_DENOMINATOR_ULSU | unsigned long | Denominator Spannungsüberwachung LSU Bank 1 |
| STAT_NUMERATOR_ULSU2 | unsigned long | Numerator Spannungsüberwachung LSU Bank 2 |
| STAT_DENOMINATOR_ULSU2 | unsigned long | Denominator Spannungsüberwachung LSU Bank 2 |
| STAT_NUMERATOR_PLLSU | unsigned long | Numerator Plausibilität LSU Bank 1 |
| STAT_DENOMINATOR_PLLSU | unsigned long | Denominator Plausibilität LSU Bank 1 |
| STAT_NUMERATOR_PLLSU2 | unsigned long | Numerator Plausibilität LSU Bank 2 |
| STAT_DENOMINATOR_PLLSU2 | unsigned long | Denominator Plausibilität LSU Bank 2 |
| STAT_NUMERATOR_TES | unsigned long | Numerator Tankentlüftungssystem |
| STAT_DENOMINATOR_TES | unsigned long | Denominator Tankentlüftungssystem |
| STAT_NUMERATOR_TESG | unsigned long | Numerator Tankdiagnose Grobleck |
| STAT_DENOMINATOR_TESG | unsigned long | Denominator Tankdiagnose Grobleck |
| STAT_NUMERATOR_DMTK | unsigned long | Numerator Tankdiagnose Feinstleck |
| STAT_DENOMINATOR_DMTK | unsigned long | Denominator Tankdiagnose Feinstleck |
| STAT_NUMERATOR_DMTL | unsigned long | Numerator Tankdiagnose Modulfehler |
| STAT_DENOMINATOR_DMTL | unsigned long | Denominator Tankdiagnose Modulfehler |
| STAT_NUMERATOR_ENWS | unsigned long | Numerator NKW-Einlaß Bank 1 |
| STAT_DENOMINATOR_ENWS | unsigned long | Denominator NKW-Einlaß Bank 1 |
| STAT_NUMERATOR_ANWS | unsigned long | Numerator NKW-Auslaß Bank 1 |
| STAT_DENOMINATOR_ANWS | unsigned long | Denominator NKW-Auslaß Bank 1 |
| STAT_NUMERATOR_ENWS2 | unsigned long | Numerator NKW-Einlaß Bank 2 |
| STAT_DENOMINATOR_ENWS2 | unsigned long | Denominator NKW-Einlaß Bank 2 |
| STAT_NUMERATOR_ANWS2 | unsigned long | Numerator NKW-Auslaß Bank 2 |
| STAT_DENOMINATOR_ANWS2 | unsigned long | Denominator NKW-Auslaß Bank 2 |
| STAT_NUMERATOR_ENWSAD | unsigned long | Numerator Einlassnockenwellensteuerung Anschlagsadaption Bank 1 |
| STAT_DENOMINATOR_ENWSAD | unsigned long | Denominator Einlassnockenwellensteuerung Anschlagsadaption Bank 1 |
| STAT_NUMERATOR_ENWSAD2 | unsigned long | Numerator Einlassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_DENOMINATOR_ENWSAD2 | unsigned long | Denominator Einlassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_NUMERATOR_ANWSAD | unsigned long | Numerator Auslassnockenwellensteuerung Anschlagsadaption Bank 1 |
| STAT_DENOMINATOR_ANWSAD | unsigned long | Denominator Auslassnockenwellensteuerung Anschlagsadaption Bank 1 |
| STAT_NUMERATOR_ANWSAD2 | unsigned long | Numerator Auslassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_DENOMINATOR_ANWSAD2 | unsigned long | Denominator Auslassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_NUMERATOR_NWEKW | unsigned long | Numerator Zuordnung Einlassnockenwelle zu Kurbelwelle Bank 1 |
| STAT_DENOMINATOR_NWEKW | unsigned long | Denominator Zuordnung Einlassnockenwelle zu Kurbelwelle Bank 1 |
| STAT_NUMERATOR_NWEKW2 | unsigned long | Numerator Zuordnung Einlassnockenwelle Bank zu Kurbelwelle Bank 2 |
| STAT_DENOMINATOR_NWEKW2 | unsigned long | Denominator Zuordnung Einlassnockenwelle Bank zu Kurbelwelle Bank 2 |
| STAT_NUMERATOR_NWAKW | unsigned long | Numerator Zuordnung Auslassnockenwelle zu Kurbelwelle Bank 1 |
| STAT_DENOMINATOR_NWAKW | unsigned long | Denominator Zuordnung Auslassnockenwelle zu Kurbelwelle Bank 1 |
| STAT_NUMERATOR_NWAKW2 | unsigned long | Numerator Zuordnung Auslassnockenwelle Bank zu Kurbelwelle Bank 2 |
| STAT_DENOMINATOR_NWAKW2 | unsigned long | Denominator Zuordnung Auslassnockenwelle Bank zu Kurbelwelle Bank 2 |
| STAT_NUMERATOR_HFMPL | unsigned long | Numerator Plausibilisierung Luftmassenmesser |
| STAT_DENOMINATOR_HFMPL | unsigned long | Denominator Plausibilisierung Luftmassenmesser |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmme2"></a>
### STATUS_RBMME2

0x22402A STATUS_RBMME2 Lesen der RBM-Werte Block2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUMERATOR_CUHR | unsigned long | Numerator CAN relativer Zeitgeber |
| STAT_DENOMINATOR_CUHR | unsigned long | Denominator CAN relativer Zeitgeber |
| STAT_NUMERATOR_HSHK | unsigned long | Numerator Heizung Lambdasonde hinter Katalysator Bank 1 |
| STAT_DENOMINATOR_HSHK | unsigned long | Denominator Heizung Lambdasonde hinter Katalysator Bank 1 |
| STAT_NUMERATOR_HSHK2 | unsigned long | Numerator Heizung Lambdasonde hinter Katalysator Bank 2 |
| STAT_DENOMINATOR_HSHK2 | unsigned long | Denominator Heizung Lambdasonde hinter Katalysator Bank 2 |
| STAT_NUMERATOR_HSV | unsigned long | Numerator Heizung Lambdasonde vor Katalysator Bank 1 |
| STAT_DENOMINATOR_HSV | unsigned long | Denominator Heizung Lambdasonde vor Katalysator Bank 1 |
| STAT_NUMERATOR_HSV2 | unsigned long | Numerator Heizung Lambdasonde vor Katalysator Bank 2 |
| STAT_DENOMINATOR_HSV2 | unsigned long | Denominator Heizung Lambdasonde vor Katalysator Bank 2 |
| STAT_NUMERATOR_LASH | unsigned long | Numerator Lambdasondenalterung hinter Katalysator Bank 1 |
| STAT_DENOMINATOR_LASH | unsigned long | Denominator Lambdasondenalterung hinter Katalysator Bank 1 |
| STAT_NUMERATOR_LASH2 | unsigned long | Numerator Lambdasondenalterung hinter Katalysator Bank 2 |
| STAT_DENOMINATOR_LASH2 | unsigned long | Denominator Lambdasondenalterung hinter Katalysator Bank 2 |
| STAT_NUMERATOR_LLR | unsigned long | Numerator Leerlaufregelung |
| STAT_DENOMINATOR_LLR | unsigned long | Denominator Leerlaufregelung |
| STAT_NUMERATOR_PUR | unsigned long | Numerator Umgebungsdrucksensor |
| STAT_DENOMINATOR_PUR | unsigned long | Denominator Umgebungsdrucksensor |
| STAT_NUMERATOR_TFA | unsigned long | Numerator TFA-Sensor |
| STAT_DENOMINATOR_TFA | unsigned long | Denominator TFA-Sensor |
| STAT_NUMERATOR_TKA | unsigned long | Numerator Temperatur Kühlerausgang |
| STAT_DENOMINATOR_TKA | unsigned long | Denominator Temperatur Kühlerausgang |
| STAT_NUMERATOR_TM | unsigned long | Numerator Motortemperatur |
| STAT_DENOMINATOR_TM | unsigned long | Denominator Motortemperatur |
| STAT_NUMERATOR_TUM | unsigned long | Numerator Umgebungstemperatur |
| STAT_DENOMINATOR_TUM | unsigned long | Denominator Umgebungstemperatur |
| STAT_NUMERATOR_VFZ | unsigned long | Numerator Geschwindigkeitssignal |
| STAT_DENOMINATOR_VFZ | unsigned long | Denominator Geschwindigkeitssignal |
| STAT_NUMERATOR_DVEF | unsigned long | Numerator DV-E Fehler bei Federprüfung |
| STAT_DENOMINATOR_DVEF | unsigned long | Denominator DV-E Fehler bei Federprüfung |
| STAT_NUMERATOR_DVEL | unsigned long | Numerator DV-E Lageabweichung |
| STAT_DENOMINATOR_DVEL | unsigned long | Denominator DV-E Lageabweichung |
| STAT_NUMERATOR_DVER | unsigned long | Numerator DV-E Regelbereich |
| STAT_DENOMINATOR_DVER | unsigned long | Denominator DV-E Regelbereich |
| STAT_NUMERATOR_FST | unsigned long | Numerator Tankfüllstandssensor |
| STAT_DENOMINATOR_FST | unsigned long | Denominator Tankfüllstandssensor |
| STAT_NUMERATOR_LM | unsigned long | Numerator Hauptfüllungssignal |
| STAT_DENOMINATOR_LM | unsigned long | Denominator Hauptfüllungssignal |
| STAT_NUMERATOR_DK | unsigned long | Numerator DK-Potentiometer |
| STAT_DENOMINATOR_DK | unsigned long | Denominator DK-Potentiometer |
| STAT_NUMERATOR_DK1P | unsigned long | Numerator Drosselklappenpotentiometer 1 |
| STAT_DENOMINATOR_DK1P | unsigned long | Denominator Drosselklappenpotentiometer 1 |
| STAT_NUMERATOR_DK2P | unsigned long | Numerator Drosselklappenpotentiometer 2 |
| STAT_DENOMINATOR_DK2P | unsigned long | Denominator Drosselklappenpotentiometer 2 |
| STAT_NUMERATOR_KUPPL | unsigned long | Numerator Pedalwertgeber Kupplung |
| STAT_DENOMINATOR_KUPPL | unsigned long | Denominator Pedalwertgeber Kupplung |
| STAT_NUMERATOR_LLRKH | unsigned long | Numerator Leerlaufregelung während Katalysatorheizen |
| STAT_DENOMINATOR_LLRKH | unsigned long | Denominator Leerlaufregelung während Katalysatorheizen |
| STAT_NUMERATOR_TACS | unsigned long | Numerator Ansauglufttemperatur bei Kaltstart |
| STAT_DENOMINATOR_TACS | unsigned long | Denominator Ansauglufttemperatur bei Kaltstart |
| STAT_NUMERATOR_TMCS | unsigned long | Numerator Motortemperatur bei Kaltstart |
| STAT_DENOMINATOR_TMCS | unsigned long | Denominator Motortemperatur bei Kaltstart |
| STAT_NUMERATOR_DMDKH | unsigned long | Numerator Drehmomentüberwachung während Katalysatorheizen |
| STAT_DENOMINATOR_DMDKH | unsigned long | Denominator Drehmomentüberwachung während Katalysatorheizen |
| STAT_NUMERATOR_DYSH | unsigned long | Numerator Dynamikmessung Lambdasonde hinter Katalysator Bank 1 |
| STAT_DENOMINATOR_DYSH | unsigned long | Denominator Dynamikmessung Lambdasonde hinter Katalysator Bank 1 |
| STAT_NUMERATOR_DYSH2 | unsigned long | Numerator Dynamikmessung Lambdasonde hinter Katalysator Bank 2 |
| STAT_DENOMINATOR_DYSH2 | unsigned long | Denominator Dynamikmessung Lambdasonde hinter Katalysator Bank 2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-anschlag"></a>
### STEUERN_VVT_ANSCHLAG

0x312706 STEUERN_VVT_ANSCHLAG Lernen der VVT-Anschlaege Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vvt-anschlag"></a>
### STATUS_VVT_ANSCHLAG

0x211B STATUS_VVT_ANSCHLAG Status Lernen VVT-Anschlaege Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VVT_ANSCHL1 | int | Status des Lernens Bank 1 |
| STAT_VVT_ANSCHL1_TEXT | string | Status des Lernens Bank 1 |
| STAT_VVT_ANSCHL2 | int | Status des Lernens Bank 2 |
| STAT_VVT_ANSCHL2_TEXT | string | Status des Lernens Bank 2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-vvt-anschlag"></a>
### STOP_VVT_ANSCHLAG

0x322706 STOP_VVT_ANSCHLAG Ende von Lernen der VVT-Anschlaege Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-hex-lesen"></a>
### FS_HEX_LESEN

0x210A0000 FS_HEX_LESEN Fehlerspeicher auslesen als Hex Dump Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | wird die Nummer des zu lesenden Fehlers im Fehlerspeicher uebergeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| F_ANZ_INT | int | Anzahl der eingetragenen Fehler |
| FEHLER_NR_TEXT | string | Fehlernummer im Speicher |
| FS_ZEILE1 | string | 10 Byte des Fehlerspeichers als Dump |
| FS_ZEILE2 | string | naechsten 10 Byte aus FS |
| FS_ZEILE3 | string | naechsten 10 Byte aus FS |
| FS_ZEILE4 | string | naechsten 10 Byte aus FS |
| FS_ZEILE5 | string | naechsten 10 Byte aus FS |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-lang"></a>
### FS_LESEN_LANG

0x210A0000 FS_LESEN_LANG Fehlerspeicher auslesen Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | wird die Nummer des zu lesenden Fehlers uebergeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| F_ANZ_INT | int | Anzahl der eingetragenen Fehler |
| F_ORT_NR | long | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_SYMPTOM_NR | int | Gibt die Nummer der Fehlerart aus |
| F_SYMPTOM_TEXT | string | Interpretiert die Fehlerart |
| F_READY_NR | int | Gibt an, ob Readiness gesetzt |
| F_READY_TEXT | string | gibt einen Text zur Readiness aus |
| F_VORHANDEN_NR | int | Gibt die Nummer des Eintragstatuses aus |
| F_VORHANDEN_TEXT | string | gibt die Eintragsentprellung des Fehlers an |
| F_WARNUNG_NR | int | Gibt die Nummer fuer MIL EIN aus |
| F_WARNUNG_TEXT | string | gibt an, ob die MIL angesteuert wird |
| F_ART_ERW_WERT | int | gibt das FehlerarterweiterungsByte als integer zurueck |
| F_ZYKLUS_FLAG | string | gibt an, ob Zyklus-Flag gesetzt worden ist |
| F_AKTIV_FLAG | string | gibt an, ob Diagnose laeuft |
| F_STOP_FLAG | string | gibt an, ob Stopbedingungen vorliegen |
| F_ERROR_FLAG | string | zeigt Error-Flag an |
| F_MIL_FLAG | string | zeigt den MIL-Status an |
| F_ENTPRELL_FLAG | string | gibt den MIL-Entprellstatus an |
| F_CLA | int | Klasse |
| F_FLC | int | Wert Entprellvorgaenge FLC |
| F_HLC | int | Wert Entprellvorgaenge HLC |
| F_LZ | int | Wert Loeschvorgaenge DLC |
| F_TSF | real | Wert Schwerezaehler TSF |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_KM_FIRST | string | Km-Stand bei Erstauftreten des Fehlers |
| F_KM_NEXT | string | Km-Stand beim vorletzten Auftreten des Fehlers |
| F_KM_LAST | string | Km-Stand beim letzten Auftreten des Fehlers |
| F_KM_FIRST_WERT | real | Km-Stand bei Erstauftreten |
| F_KM_NEXT_WERT | real | Km-Stand beim vorletzten Auftreten des Fehlers |
| F_KM_LAST_WERT | real | Km-Stand beim letzten Auftreten des Fehlers |
| F_UW1_APP_NR | int | Applikationswert der 1. Umweltbedingung |
| F_UW2_APP_NR | int | Applikationswert der 2. Umweltbedingung |
| F_UW3_APP_NR | int | Applikationswert der 3. Umweltbedingung |
| F_UW4_APP_NR | int | Applikationswert der 4. Umweltbedingung |
| F_UW1_NR | int | 1.Satz Umweltbedingung 1 Index (Ersterkennung) |
| F_UW1_TEXT | string | 1.Satz UW1 Text zur Umweltbedingung |
| F_UW1_WERT | real | 1.Satz UW1 Wert der Umweltbedingung |
| F_UW1_EINH | string | 1.Satz UW1 Einheit |
| F_UW2_NR | int | 1.Satz Umweltbedingung 2 Index (Ersterkennung) |
| F_UW2_TEXT | string | 1.Satz UW2 Text zur Umweltbedingung |
| F_UW2_WERT | real | 1.Satz UW2 Wert der Umweltbedingung |
| F_UW2_EINH | string | 1.Satz UW2 Einheit |
| F_UW3_NR | int | 1.Satz Umweltbedingung 3 Index (Ersterkennung) |
| F_UW3_TEXT | string | 1.Satz UW3 Text zur Umweltbedingung |
| F_UW3_WERT | real | 1.Satz UW3 Wert der Umweltbedingung |
| F_UW3_EINH | string | 1.Satz UW3 Einheit |
| F_UW4_NR | int | 1.Satz Umweltbedingung 4 Index (Ersterkennung) |
| F_UW4_TEXT | string | 1.Satz UW4 Text zur Umweltbedingung |
| F_UW4_WERT | real | 1.Satz UW4 Wert der Umweltbedingung |
| F_UW4_EINH | string | 1.Satz UW4 Einheit |
| F_UW5_NR | int | 2.Satz Umweltbedingung 1 Index (zweite Erkennung) |
| F_UW5_TEXT | string | 2.Satz UW1 Text zur Umweltbedingung |
| F_UW5_WERT | real | 2.Satz UW1 Wert der Umweltbedingung |
| F_UW5_EINH | string | 2.Satz UW1 Einheit |
| F_UW6_NR | int | 2.Satz Umweltbedingung 2 Index (zweite Erkennung) |
| F_UW6_TEXT | string | 2.Satz UW2 Text zur Umweltbedingung |
| F_UW6_WERT | real | 2.Satz UW2 Wert der Umweltbedingung |
| F_UW6_EINH | string | 2.Satz UW2 Einheit |
| F_UW7_NR | int | 2.Satz Umweltbedingung 3 Index (zweite Erkennung) |
| F_UW7_TEXT | string | 2.Satz UW3 Text zur Umweltbedingung |
| F_UW7_WERT | real | 2.Satz UW3 Wert der Umweltbedingung |
| F_UW7_EINH | string | 2.Satz UW3 Einheit |
| F_UW8_NR | int | 2.Satz Umweltbedingung 4 Index (zweite Erkennung) |
| F_UW8_TEXT | string | 2.Satz UW4 Text zur Umweltbedingung |
| F_UW8_WERT | real | 2.Satz UW4 Wert der Umweltbedingung |
| F_UW8_EINH | string | 2.Satz UW4 Einheit |
| F_UW9_NR | int | 3.Satz Umweltbedingung 1 Index (aktuelle Erkennung) |
| F_UW9_TEXT | string | 3.Satz UW1 Text zur Umweltbedingung |
| F_UW9_WERT | real | 3.Satz UW1 Wert der Umweltbedingung |
| F_UW9_EINH | string | 3.Satz UW1 Einheit |
| F_UW10_NR | int | 3.Satz Umweltbedingung 2 Index (aktuelle Erkennung) |
| F_UW10_TEXT | string | 3.Satz UW2 Text zur Umweltbedingung |
| F_UW10_WERT | real | 3.Satz UW2 Wert der Umweltbedingung |
| F_UW10_EINH | string | 3.Satz UW2 Einheit |
| F_UW11_NR | int | 3.Satz Umweltbedingung 3 Index (aktuelle Erkennung) |
| F_UW11_TEXT | string | 3.Satz UW3 Text zur Umweltbedingung |
| F_UW11_WERT | real | 3.Satz UW3 Wert der Umweltbedingung |
| F_UW11_EINH | string | 3.Satz UW3 Einheit |
| F_UW12_NR | int | 3.Satz Umweltbedingung 4 Index (aktuelle Erkennung) |
| F_UW12_TEXT | string | 3.Satz UW4 Text zur Umweltbedingung |
| F_UW12_WERT | real | 3.Satz UW4 Wert der Umweltbedingung |
| F_UW12_EINH | string | 3.Satz UW4 Einheit |
| F_FF1_WERT | int | Freeze Frame Umweltbedingung 1 Wert |
| F_FF1_TEXT | string | Freeze Frame Umweltbedingung 1 |
| F_FF1_BESCH | string | Freeze Frame Umweltbedingung 1 Beschreibung |
| F_FF2_WERT | int | Freeze Frame Umweltbedingung 2 Wert |
| F_FF2_TEXT | string | Freeze Frame Umweltbedingung 2 Text |
| F_FF2_BESCH | string | Freeze Frame Umweltbedingung 2 Beschreibung |
| F_FF3_TEXT | string | Freeze Frame Umweltbedingung 3 Text |
| F_FF3_EINH | string | Freeze Frame Umweltbedingung 3 Einheit |
| F_FF3_WERT | real | Freeze Frame Umweltbedingung 3 Wert |
| F_FF4_TEXT | string | Freeze Frame Umweltbedingung 4 Text |
| F_FF4_EINH | string | Freeze Frame Umweltbedingung 4 EINH |
| F_FF4_WERT | real | Freeze Frame Umweltbedingung 4  Wert |
| F_FF5_TEXT | string | Freeze Frame Umweltbedingung 5 Text |
| F_FF5_EINH | string | Freeze Frame Umweltbedingung 5 EINH |
| F_FF5_WERT | real | Freeze Frame Umweltbedingung 5  Wert |
| F_FF6_TEXT | string | Freeze Frame Umweltbedingung 6 Text |
| F_FF6_EINH | string | Freeze Frame Umweltbedingung 6 EINH |
| F_FF6_WERT | real | Freeze Frame Umweltbedingung 6  Wert |
| F_FF7_TEXT | string | Freeze Frame Umweltbedingung 7 Text |
| F_FF7_EINH | string | Freeze Frame Umweltbedingung 7 EINH |
| F_FF7_WERT | real | Freeze Frame Umweltbedingung 7  Wert |
| F_FF8_TEXT | string | Freeze Frame Umweltbedingung 8 Text |
| F_FF8_EINH | string | Freeze Frame Umweltbedingung 8 EINH |
| F_FF8_WERT | real | Freeze Frame Umweltbedingung 8  Wert |
| F_FF9_TEXT | string | Freeze Frame Umweltbedingung 9 Text |
| F_FF9_EINH | string | Freeze Frame Umweltbedingung 9 EINH |
| F_FF9_WERT | real | Freeze Frame Umweltbedingung 9  Wert |
| F_FF10_TEXT | string | Freeze Frame Umweltbedingung 10 Text |
| F_FF10_EINH | string | Freeze Frame Umweltbedingung 10 EINH |
| F_FF10_WERT | real | Freeze Frame Umweltbedingung 10  Wert |
| F_FF11_TEXT | string | Freeze Frame Umweltbedingung 11 Text |
| F_FF11_EINH | string | Freeze Frame Umweltbedingung 11 EINH |
| F_FF11_WERT | real | Freeze Frame Umweltbedingung 11  Wert |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_P_CODE | string | P-Code des eingetragenen Fehlers |
| F_HEX_CODE | binary | Hexdump des Fehlers |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-1"></a>
### STEUERN_EV_1

0x30CB07FF STEUERN_EV_1 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-2"></a>
### STEUERN_EV_2

0x30CC07FF STEUERN_EV_2 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-3"></a>
### STEUERN_EV_3

0x30CD07FF STEUERN_EV_3 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-4"></a>
### STEUERN_EV_4

0x30CE07FF STEUERN_EV_4 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-5"></a>
### STEUERN_EV_5

0x30CF07FF STEUERN_EV_5 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-6"></a>
### STEUERN_EV_6

0x30D107FF STEUERN_EV_6 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-7"></a>
### STEUERN_EV_7

0x30D207FF STEUERN_EV_7 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-8"></a>
### STEUERN_EV_8

0x30D307FF STEUERN_EV_8 Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | sHex-Antwort von SG |

<a id="job-steuern-ev-1-aus"></a>
### STEUERN_EV_1_AUS

0x30CB00 STEUERN_EV_1_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-2-aus"></a>
### STEUERN_EV_2_AUS

0x30CC00 STEUERN_EV_2_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-3-aus"></a>
### STEUERN_EV_3_AUS

0x30CD00 STEUERN_EV_3_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-4-aus"></a>
### STEUERN_EV_4_AUS

0x30CE00 STEUERN_EV_4_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-5-aus"></a>
### STEUERN_EV_5_AUS

0x30CF00 STEUERN_EV_5_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-6-aus"></a>
### STEUERN_EV_6_AUS

0x30D100 STEUERN_EV_6_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-7-aus"></a>
### STEUERN_EV_7_AUS

0x30D200 STEUERN_EV_7_AUS Stellgliedansteuerung Einspritzventile deaktivieren Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-8-aus"></a>
### STEUERN_EV_8_AUS

0x30D300 STEUERN_EV_8_AUS Stellgliedansteuerung Einspritzventile Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

0x30C10700 STEUERN_E_LUEFTER Stellgliedansteuerung E-Luefter Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTRATE | int | zwischen 0 und 100 % Ansteuerverhaeltins |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter-aus"></a>
### STEUERN_E_LUEFTER_AUS

0x30C100 STEUERN_E_LUEFTER_AUS Stellgliedansteuerung E-Luefter Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev"></a>
### START_SYSTEMCHECK_TEV

0x312200 START_SYSTEMCHECK_TEV Systemtest von TEV Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-tev"></a>
### STATUS_SYSTEMCHECK_TEV

0x2112 STATUS_SYSTEMCHECK_TEV Status Systemtest TEV Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_TEV_WERT | int | Status der TEV-Diagnose |
| STAT_SYSTEMCHECK_TEV_TEXT | string | Status der TEV-Diagnose |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev"></a>
### STOP_SYSTEMCHECK_TEV

0x322200 STOP_SYSTEMCHECK_TEV Beenden von TEV-Systemtest Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev-aus"></a>
### STEUERN_TEV_AUS

0x30C500 STEUERN_TEV_AUS Stellgliedansteuerung TEV vom Tester an DME freigeben Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

0x30C50704 STEUERN_TEV Stellgliedansteuerung TEV Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANSTEUERRATE | int | Sollwert 0 - 100% |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kfk"></a>
### STEUERN_KFK

0x30C307FF STEUERN_KFK Stellgliedansteuerung KFK Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kfk-aus"></a>
### STEUERN_KFK_AUS

0x30C300 STEUERN_KFK_AUS Stellgliedansteuerung KFK Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mil"></a>
### STEUERN_MIL

0x30F107FF STEUERN_MIL Ansteuerung MIL (MIL blinken) Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mil-aus"></a>
### STEUERN_MIL_AUS

0x30F100 STEUERN_MIL_AUS Beenden der MIL-Ansteuerung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eml"></a>
### STEUERN_EML

0x30F307FF STEUERN_EML Stellgliedansteuerung EML Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eml-aus"></a>
### STEUERN_EML_AUS

0x30F300 STEUERN_EML_AUS Beenden der Stellgliedansteuerung EML Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

0xC607FF STEUERN_EKP Stellgliedansteuerung EKP Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp-aus"></a>
### STEUERN_EKP_AUS

0x30C600 STEUERN_EKP_AUS Stellgliedansteuerung EKP Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls1"></a>
### STEUERN_HLS1

0x30C70705 STEUERN_HLS1 Stellgliedansteuerung Lambdasondenheizung 1 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls1-aus"></a>
### STEUERN_HLS1_AUS

0x30C700 STEUERN_HLS1_AUS Stellgliedansteuerung Lambdasondeheizung 1 aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls2"></a>
### STEUERN_HLS2

0x30C80705 STEUERN_HLS2 Stellgliedansteuerung Lambdasondenheizung 2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls2-aus"></a>
### STEUERN_HLS2_AUS

0x30C800 STEUERN_HLS2_AUS Stellgliedansteuerung Lambdasondeheizung 2 aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls3"></a>
### STEUERN_HLS3

0x30C90705 STEUERN_HLS3 Stellgliedansteuerung Lambdasondenheizung 3 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls3-aus"></a>
### STEUERN_HLS3_AUS

0x30C900 STEUERN_HLS3_AUS Stellgliedansteuerung Lambdasondeheizung 3 aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls4"></a>
### STEUERN_HLS4

0x30CA0705 STEUERN_HLS4 Stellgliedansteuerung Lambdasondenheizung 4 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls4-aus"></a>
### STEUERN_HLS4_AUS

0x30CA00 STEUERN_HLS4_AUS Stellgliedansteuerung Lambdasondeheizung 4 aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl"></a>
### STEUERN_EBL

0x30D807FF STEUERN_EBL Stellgliedansteuerung E-Box-Luefter Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl-aus"></a>
### STEUERN_EBL_AUS

0x30D800 STEUERN_EBL_AUS Stellgliedansteuerung E-Box-Luefter aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

0x30D90700 STEUERN_AGK Stellgliedansteuerung Abgasklappe Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk-aus"></a>
### STEUERN_AGK_AUS

0x30D900 STEUERN_AGK_AUS Stellgliedansteuerung Abgasklappe aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlp"></a>
### STEUERN_DMTLP

0x30DA07FF STEUERN_DMTLP Stellgliedansteuerung DM-TL Pumpe Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlp-aus"></a>
### STEUERN_DMTLP_AUS

0x30DA00 STEUERN_DMTLP_AUS Stellgliedansteuerung DM-TL Pumpe aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlv"></a>
### STEUERN_DMTLV

0x30DB07FF STEUERN_DMTLV Stellgliedansteuerung DM-TL Ventil Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlv-aus"></a>
### STEUERN_DMTLV_AUS

0x30DB00 STEUERN_DMTLV_AUS Stellgliedansteuerung DM-TL Ventil aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlh"></a>
### STEUERN_DMTLH

0x30F407FF STEUERN_DMTLH Ansteuerung DMTL-Heizung (nur bei US-Fahrzeugen) Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlh-aus"></a>
### STEUERN_DMTLH_AUS

0x30F400 STEUERN_DMTLH_AUS Beenden Ansteuerung DMTL-Heizung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ram-backup"></a>
### RAM_BACKUP

0x31E900 RAM_BACKUP Loeschen der RAM-Backup-Werte Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zwang-rambackup"></a>
### STEUERN_ZWANG_RAMBACKUP

0x31F200 STEUERN_ZWANG_RAMBACKUP Zwangssichern der RAM-Backup-Werte Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

0x312600 START_SYSTEMCHECK_LLERH Diagnosefunktion LL-Erhoehung Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_WERT | int | Eingabewert: 0...1200 wg. Begr. i. PST sind nur Werte zw. 400 Upmin u. 1200 Upmin wirksam |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-llerh"></a>
### STATUS_SYSTEMCHECK_LLERH

0x2116 STATUS_SYSTEMCHECK_LLERH Diagnosefunktion LL-Erhoehung Status lesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LL_TEXT | string | Status der Diagnose |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

0x322600 STOP_SYSTEMCHECK_LLERH Diagnosefunktion LL-Erhoehung Status lesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

0x31DA00 START_SYSTEMCHECK_DMTL Start Systemtest DMTL Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dmtl"></a>
### STATUS_SYSTEMCHECK_DMTL

0x2119 STATUS_SYSTEMCHECK_DMTL Status Systemtest DMTL Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POINTER_VALUE | int | Wert des Zustandspointer der DMTL-Diagnose |
| STAT_POINTER | string | Zustandspointer der DMTL-Diagnose |
| STAT_POINTER_FREEZE | string | Zustandspointer der DMTL-Diagnose |
| STAT_POINTER_FREEZE_VALUE | int | Zustandspointer der DMTL-Diagnose |
| STAT_DMTLDIAG_TEXT | string | Status der DMTL-Diagnose |
| STAT_IPTESKF_TEXT | string | Pumpenstrom DM-TL gefiltert |
| STAT_IPGLMN_TEXT | string | minimaler Pumpenstrom Grobleckmessung |
| STAT_IPTREF_TEXT | string | Pumpenstrom Referenzleck |
| STAT_IPTESKF_WERT | real | Pumpenstrom DM-TL gefiltert |
| STAT_IPGLMN_WERT | real | minimaler Pumpenstrom Grobleckmessung |
| STAT_IPTREF_WERT | real | Pumpenstrom Referenzleck |
| STAT_IPT_EINH | string | Einheit der Stroeme |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

0x32DA00 STOP_SYSTEMCHECK_DMTL Ende Systemtest DM-TL Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-einlass"></a>
### STEUERN_VANOS_EINLASS

0x30E30700 STEUERN_VANOS_EINLASS Stellgliedansteuerung Einlass-VANOS Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | real | gibt den Verstellwinkel an (-102..102) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-einlass-aus"></a>
### STEUERN_VANOS_EINLASS_AUS

0x30E300 STEUERN_VANOS_EINLASS_AUS Stellgliedansteuerung Einlass-VANOS freigeben Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-auslass"></a>
### STEUERN_VANOS_AUSLASS

0x30E40700 STEUERN_VANOS_AUSLASS Stellgliedansteuerung Auslass-VANOS Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | real | gibt den Verstellwinkel an (-102..102) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-auslass-aus"></a>
### STEUERN_VANOS_AUSLASS_AUS

0x30E400 STEUERN_VANOS_AUSLASS_AUS Stellgliedansteuerung Auslass-VANOS freigeben Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa"></a>
### STEUERN_DISA

0x30E60700 STEUERN_DISA Stellgliedansteuerung DISA Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | gibt den Verstellwinkel an (0..100) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa-aus"></a>
### STEUERN_DISA_AUS

0x30E600 STEUERN_DISA_AUS Stellgliedansteuerung DISA freigeben Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-evausbl"></a>
### STEUERN_EVAUSBL

0x312500 STEUERN_EVAUSBL Systemdiagnose Einspritzventile ausblenden Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR | int | Ausblendung Einspritzventile evz_austot   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-evausbl-aus"></a>
### STEUERN_EVAUSBL_AUS

0x322500 STEUERN_EVAUSBL_AUS Ende Systemtest Einspritzventile ausblenden Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR | int | gibt die Ventile (binaer, jedes Bit ein EV) an, die ausgeblendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

0x224000 STATUS_MESSWERTE Auslesen von Messwerten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TE_WERT | real | Wert von te_w (effektive Einspritzzeit) |
| STAT_TE_EINH | string | Einheit von te_w (effektive Einspritzzeit) |
| STAT_FR_WERT | real | Wert von fr_w (Lambdaregler-Ausgang) |
| STAT_FR_EINH | string | Einheit von fr_w (Lambdaregler-Ausgang) |
| STAT_FR2_WERT | real | Wert von fr2_w (Lambdaregler-Ausgang Bank 2) |
| STAT_FR2_EINH | string | Einheit von fr2_w (Lambdaregler-Ausgang) |
| STAT_VFZG_WERT | real | Wert von vfzg (Fahrzeuggeschwindigkeit) |
| STAT_VFZG_EINH | string | Einheit von vfzg (Fahrzeuggeschwindigkeit) |
| STAT_NMOT_WERT | real | Wert von nmot_w (Motordrehzahl) |
| STAT_NMOT_EINH | string | Einheit von nmot_w (Motordrehzahl) |
| STAT_NSOL_WERT | real | Wert von nsol (Leerlauf-Solldrehzahl) |
| STAT_NSOL_EINH | string | Einheit von nsol (Leerlauf-Solldrehzahl) |
| STAT_WNWKWE_WERT | real | Wert von wnwkwe_w (Winkel Einlaß-NW-Flanke rel. z. KW) |
| STAT_WNWKWE_EINH | string | Einheit von wnwkwe_w (Winkel Einlaß-NW-Flanke rel. z. KW) |
| STAT_WNWKWA_WERT | real | Wert von wnwkwa_w (Winkel Auslaß-NW-Flanke rel. z. KW) |
| STAT_WNWKWA_EINH | string | Einheit von wnwkwa_w (Winkel Auslaß-NW-Flanke rel. z. KW) |
| STAT_TANS_WERT | real | Wert von tans (Ansauglufttemperatur) |
| STAT_TANS_EINH | string | Einheit von tans (Ansauglufttemperatur) |
| STAT_TMOT_WERT | real | Wert von tmot (Motortemperatur) |
| STAT_TMOT_EINH | string | Einheit von tmot (Motortemperatur) |
| STAT_ZWOUT_WERT | real | Wert von zwout (Zündwinkelausgabe) |
| STAT_ZWOUT_EINH | string | Einheit von zwout (Zündwinkelausgabe) |
| STAT_WDKBA_WERT | real | Wert von wdkba (DK Winkel rel. z. unteren Anschlag) |
| STAT_WDKBA_EINH | string | Einheit von wdkba (DK Winkel rel. z. unteren Anschlag) |
| STAT_MSHFM_WERT | real | Wert von mshfm_w (Massenstrom) |
| STAT_MSHFM_EINH | string | Einheit von mshfm_w (Massenstrom) |
| STAT_MIIST_WERT | real | Wert von miist_w (indiziertes Motormoment) |
| STAT_MIIST_EINH | string | Einheit von miist_w (indiziertes Motormoment) |
| STAT_UB_WERT | real | Wert von ub (Batteriespannung) |
| STAT_UB_EINH | string | Einheit von ub (Batteriespannung) |
| STAT_UPWG_WERT | real | Wert von upwg1_w (Spannung PWG-Poti 1) |
| STAT_UPWG_EINH | string | Einheit von upwg1_w (Spannung PWG-Poti 1) |
| STAT_TKA_WERT | real | Wert von tkalin (Temperatur Kühlerausgang) |
| STAT_TKA_EINH | string | Einheit von tkalin (Temperatur Kühlerausgang) |
| STAT_RKRN0_WERT | real | Wert von rkrn_w[0] (normierter Referenzpegel Klopfsensor 1) |
| STAT_RKRN0_EINH | string | Einheit von rkrn_w[0] (normierter Referenzpegel Klopfsensor 1) |
| STAT_RKRN1_WERT | real | Wert von rkrn_w[1] (normierter Referenzpegel Klopfsensor 2) |
| STAT_RKRN1_EINH | string | Einheit von rkrn_w[1] (normierter Referenzpegel Klopfsensor 2) |
| STAT_RKRN2_WERT | real | Wert von rkrn_w[2] (normierter Referenzpegel Klopfsensor 3) |
| STAT_RKRN2_EINH | string | Einheit von rkrn_w[2] (normierter Referenzpegel Klopfsensor 3) |
| STAT_RKRN3_WERT | real | Wert von rkrn_w[3] (normierter Referenzpegel Klopfsensor 4) |
| STAT_RKRN3_EINH | string | Einheit von rkrn_w[3] (normierter Referenzpegel Klopfsensor 4) |
| STAT_RKRN4_WERT | real | Wert von rkrn_w[4] (normierter Referenzpegel Klopfsensor 5) |
| STAT_RKRN4_EINH | string | Einheit von rkrn_w[4] (normierter Referenzpegel Klopfsensor 5) |
| STAT_RKRN5_WERT | real | Wert von rkrn_w[5] (normierter Referenzpegel Klopfsensor 6) |
| STAT_RKRN5_EINH | string | Einheit von rkrn_w[5] (normierter Referenzpegel Klopfsensor 6) |
| STAT_RKRN6_WERT | real | Wert von rkrn_w[6] (normierter Referenzpegel Klopfsensor 7) |
| STAT_RKRN6_EINH | string | Einheit von rkrn_w[6] (normierter Referenzpegel Klopfsensor 7) |
| STAT_RKRN7_WERT | real | Wert von rkrn_w[7] (normierter Referenzpegel Klopfsensor 8) |
| STAT_RKRN7_EINH | string | Einheit von rkrn_w[7] (normierter Referenzpegel Klopfsensor 8) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-oel"></a>
### STATUS_MESSWERTE_OEL

0x224000 STATUS_MESSWERTE_OEL Auslesen von Oelwerten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_OELNIV_KURZMITTEL_WERT | real | Wert von oznivkrzt (Kurzmittelwert Ölniveau) |
| STAT_OELNIV_KURZMITTEL_EINH | string | Einheit von oznivkrzt (Kurzmittelwert Ölniveau) |
| STAT_OELNIV_LANGMITTEL_WERT | real | Wert von oznivlangt (Langmittelwert Ölniveau) |
| STAT_OELNIV_LANGMITTEL_EINH | string | Einheit von oznivlangt (Langmittelwert Ölniveau) |
| _TEL_AUFTRAG_BERECHNETE_WERTE | binary | Hex-Auftrag an SG (Auftrag f. oznivkrzt u. oznivlangt) |
| _TEL_ANTWORT_BERECHNETE_WERTE | binary | Hex-Antwort von SG (Antwort f. oznivkrzt u. oznivlangt) |
| STAT_OELNIV_SENSOR_WERT | real | Wert von oznivakt (Sensorwert Ölniveau) |
| STAT_OELNIV_SENSOR_EINH | string | Einheit von oznivakt (Sensorwert Ölniveau) |
| STAT_OELTEMP_SENSOR_WERT | real | Wert von oztmpakt_w (Sensorwert Oeltemperatur) |
| STAT_OELTEMP_SENSOR_EINH | string | Einheit von oztmpakt_w (Sensorwert Oeltemperatur) |
| STAT_OELPERM_SENSOR_WERT | real | Wert von ozprmakt_w (Sensorwert Oelpermitivitaet) |
| STAT_OELPERM_SENSOR_EINH | string | Einheit von ozprmakt_w (Sensorwert Oelpermitivitaet) |
| _TEL_AUFTRAG_SENSOR_WERTE | binary | Hex-Auftrag an SG (Auftrag f. oznivakt, oztmpakt_w u. ozprmakt_w) |
| _TEL_ANTWORT_SENSOR_WERTE | binary | Hex-Antwort von SG (Antwort f. oznivakt, oztmpakt_w u. ozprmakt_w) |

<a id="job-status-batterieintegrator"></a>
### STATUS_BATTERIEINTEGRATOR

0x224001 STATUS_BATTERIEINTEGRATOR Auslesen des Batterie-Ladezustands Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DFMONITOR_WERT | real | Wert von dfmonitor (Batterie-Ladezustand) |
| STAT_DFMONITOR_EINH | string | Einheit von dfmonitor (Batterie-Ladezustand) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schalterstati"></a>
### STATUS_SCHALTERSTATI

0x224002 STATUS_SCHALTERSTATI Auslesen von SchalterStatusflags Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KL15_EIN | int | Status B_kl15 (Bedingung KL15 an) |
| STAT_ESTART_EIN | int | Status B_estart (Bedingung Startrelais) |
| STAT_KUPPL_EIN | int | Status B_kuppl (Bedingung Kupplung betaetigt) |
| STAT_BL_EIN | int | Status B_bl (Bedingung Bremslichtschalter ein) |
| STAT_BR_EIN | int | Status B_br (Bedingung Bremstestschalter ein) |
| STAT_KO_EIN | int | Status B_ko (Bedingung Klimakompressor ein) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-funktionsstati"></a>
### STATUS_FUNKTIONSSTATI

0x224007 STATUS_FUNKTIONSSTATI Auslesen der Funktionsstati Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_LL_EIN | int | Status B_ll (Bedingung Leerlauf) |
| STAT_VL_EIN | int | Status B_vl (Bedingung Vollast) |
| STAT_SBBHK2_EIN | int | Status B_sbbhk2 (Bedingung Lambdasondenbereitschaft hinter Kat Bank 2) |
| STAT_SBBHK_EIN | int | Status B_sbbhk (Bedingung Lambdasondenbereitschaft hinter Kat) |
| STAT_SBBVK2_EIN | int | Status B_sbbvk2 (Bedingung Lambdasondenbereitschaft vor Kat Bank 2) |
| STAT_SBBVK_EIN | int | Status B_sbbvk (Bedingung Lambdasondenbereitschaft vor Kat) |
| STAT_LR2_EIN | int | Status B_lr2 (Bedingung Lambdaregelung Bank 2 ein) |
| STAT_LR_EIN | int | Status B_lr (Bedingung Lambdaregelung ein) |
| STAT_KD_EIN | int | Status B_kd (Bedingung KickDown ein) |
| STAT_PN_EIN | int | Status B_pn (Bedingung Park-Neutral nicht ein) |
| STAT_PEDSPORT_EIN | int | Status B_pedsport (Fahrzeug im Sportmodus) |
| STAT_ECULOCK_EIN | int | Status B_eculock (Bedingung EWS_OK ein) |
| STAT_TEHB_EIN | int | Status B_tehb (Bedingung Tankentlüftung m. hoher Beladung ein) |
| STAT_SA_EIN | int | Status B_sa (Bedingung Schubabschneiden ein) |
| STAT_LRNRDY_EIN | int | Status B_lrnrdy (Bedingung UMA Lernerfolg) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-laufunruhe"></a>
### STATUS_LAUFUNRUHE

0x224003 STATUS_LAUFUNRUHE Auslesen von Laufunruhewerten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_LUTSFI1_WERT | real | Wert von lutsfi1_w (Laufunruhewert Zylinder 1) |
| STAT_LUTSFI1_EINH | string | Einheit von lutsfi1_w (Laufunruhewert Zylinder 1) |
| STAT_LUTSFI2_WERT | real | Wert von lutsfi2_w (Laufunruhewert Zylinder 2) |
| STAT_LUTSFI2_EINH | string | Einheit von lutsfi2_w (Laufunruhewert Zylinder 2) |
| STAT_LUTSFI3_WERT | real | Wert von lutsfi3_w (Laufunruhewert Zylinder 3) |
| STAT_LUTSFI3_EINH | string | Einheit von lutsfi3_w (Laufunruhewert Zylinder 3) |
| STAT_LUTSFI4_WERT | real | Wert von lutsfi4_w (Laufunruhewert Zylinder 4) |
| STAT_LUTSFI4_EINH | string | Einheit von lutsfi4_w (Laufunruhewert Zylinder 4) |
| STAT_LUTSFI5_WERT | real | Wert von lutsfi5_w (Laufunruhewert Zylinder 5) |
| STAT_LUTSFI5_EINH | string | Einheit von lutsfi5_w (Laufunruhewert Zylinder 5) |
| STAT_LUTSFI6_WERT | real | Wert von lutsfi6_w (Laufunruhewert Zylinder 6) |
| STAT_LUTSFI6_EINH | string | Einheit von lutsfi6_w (Laufunruhewert Zylinder 6) |
| STAT_LUTSFI7_WERT | real | Wert von lutsfi7_w (Laufunruhewert Zylinder 7) |
| STAT_LUTSFI7_EINH | string | Einheit von lutsfi7_w (Laufunruhewert Zylinder 7) |
| STAT_LUTSFI8_WERT | real | Wert von lutsfi8_w (Laufunruhewert Zylinder 8) |
| STAT_LUTSFI8_EINH | string | Einheit von lutsfi8_w (Laufunruhewert Zylinder 8) |
| STAT_FOFR1_EIN | int | Wert von B_fofr1 (Bed. Adaption abgeschlossen) |
| STAT_UULSUV_WERT | real | Wert von uulsuv_w (Lambdasondenspannung 1) |
| STAT_UULSUV_EINH | string | Einheit von uulsuv_w (Lambdasondenspannung 1) |
| STAT_UULSUV2_WERT | real | Wert von uulsuv2_w (Lambdasondenspannung 2) |
| STAT_UULSUV2_EINH | string | Einheit von uulsuv2_w (Lambdasondenspannung 2) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dkhfm"></a>
### STATUS_DKHFM

0x224008 STATUS_DKHFM Auslesen von DK/HFM-Abgleichswerten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_EISYDKFKAF_WERT | real | Wert von eisydkfkaf (Abgleich DK-Modell-Faktor) |
| STAT_EISYDKKOFF_WERT | real | Wert von eisydkkoff (Abgleich DK-Modell-Offset) |
| STAT_EISYDKKOFF_EINH | string | Einheit von eisydkkoff [kg/h] |
| STAT_EISYEVFKAF_WERT | real | Wert von eisyevfkaf (Abgleich EV-Modell-Faktor) |
| STAT_EISYEVKOFF_WERT | real | Wert von eisyevkoff (Abgleich EV-Modell-Offset) |
| STAT_EISYEVKOFF_EINH | string | Einheit von eisyevkoff [kg/h] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt"></a>
### STEUERN_VVT

0x30DD07 STEUERN_VVT VVT ansteuern Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PHY_VVT_WERT | real | SW_PHY_VVT_WERT = Vorgabewert (0..180) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-aus"></a>
### STEUERN_VVT_AUS

0x30EE00 STEUERN_VVT_AUS beenden Stellgliedansteuerung VVT Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-enable"></a>
### STEUERN_VVT_ENABLE

0x30E707FF STEUERN_VVT_ENABLE Generieren eines Testsignals auf der VVT-Enable-Leitung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-enable-aus"></a>
### STEUERN_VVT_ENABLE_AUS

0x30E700 STEUERN_VVT_ENABLE_AUS Testsignal von VVT-Enable-Leitung zurücknehmen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-co-abgleich"></a>
### STATUS_CO_ABGLEICH

0x30A201 STATUS_CO_ABGLEICH Auslesen des LL-CO-Wertes Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_CO_ABGLEICH_WERT | real | LL CO-Abgleichswert |
| STAT_CO_ABGLEICH_EINH | string | Einheit des LL CO-Abgleichswertes |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-verstellen"></a>
### STEUERN_CO_ABGLEICH_VERSTELLEN

0x30A20700 STEUERN_CO_ABGLEICH_VERSTELLEN LL-CO-Wert vorgeben Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_WERT | int | LL CO-Abgleichswert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-programmieren"></a>
### STEUERN_CO_ABGLEICH_PROGRAMMIEREN

0xA20800 STEUERN_CO_ABGLEICH_PROGRAMMIEREN LL-CO-WERT programmieren Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_FEST | int | LL CO-Abgleichswert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gemisch"></a>
### STATUS_GEMISCH

0x224004 STATUS_GEMISCH Auslesen von Gemischwerten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_RKAT_WERT | real | Wert von rkat_w (Gemischadap. additiv 1) |
| STAT_RKAT_EINH | string | Einheit von rkat_w (Gemischadap. additiv 1) |
| STAT_RKAT2_WERT | real | Wert von rkat2_w (Gemischadap. additiv 2) |
| STAT_RKAT2_EINH | string | Einheit von rkat2_w (Gemischadap. additiv 2) |
| STAT_FRA_WERT | real | Wert von fra_w (Gemischadap. multip. 1) |
| STAT_FRA_EINH | string | Einheit von fra_w (Gemischadap. multip. 1) |
| STAT_FRA2_WERT | real | Wert von fra2_w (Gemischadap. multip. 2) |
| STAT_FRA2_EINH | string | Einheit von fra2_w (Gemischadap. multip. 2) |
| STAT_TEDUB_WERT | real | Wert von tedub (Einschaltdauer Heizerendstufe) |
| STAT_TEDUB_EINH | string | Einheit von tedub (Einschaltdauer Heizerendstufe) |
| STAT_TEDUB2_WERT | real | Wert von tedub2 (Einschaltdauer Heizerendstufe) |
| STAT_TEDUB2_EINH | string | Einheit von tedub2 (Einschaltdauer Heizerendstufe) |
| STAT_DYNLSU_WERT | real | Wert von dynlsu_w (norm. Dynamikwert LSU) |
| STAT_DYNLSU_EINH | string | Einheit von dynlsu_w (norm. Dynamikwert LSU) |
| STAT_DYNLSU2_WERT | real | Wert von dynlsu2_w (norm. Dynamikwert LSU 2) |
| STAT_DYNLSU2_EINH | string | Einheit von dynlsu2_w (norm. Dynamikwert LSU 2) |
| STAT_LAMSONI_WERT | real | Wert von lamsoni_w (Lambda Istwert) |
| STAT_LAMSONI_EINH | string | Einheit von lamsoni_w (Lambda Istwert) |
| STAT_LAMSONI2_WERT | real | Wert von lamsoni2_w (Lambda Istwert 2) |
| STAT_LAMSONI2_EINH | string | Einheit von lamsoni2_W (Lambda Istwert 2) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausgaenge"></a>
### STATUS_AUSGAENGE

0x224005 STATUS_AUSGAENGE Auslesen von Ausgaengen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TATEIST_WERT | real | Wert von tateist (Tastverhältnis TEV) |
| STAT_TATEIST_EINH | string | Einheit von tateist (Tastverhältnis TEV) |
| STAT_VSASPRI_WERT | real | Wert von vsa_spri (Istwert Auslasspreizung Vanos) |
| STAT_VSASPRI_EINH | string | Einheit von vsa_spri (Istwert Auslasspreizung Vanos) |
| STAT_VSASPRI2_WERT | real | Wert von vsa2spri (Istwert Auslasspreizung Vanos 2) |
| STAT_VSASPRI2_EINH | string | Einheit von vsa2spri (Istwert Auslasspreizung Vanos 2) |
| STAT_VSESPRI_WERT | real | Wert von vse_spri (Istwert Einlasspreizung Vanos) |
| STAT_VSESPRI_EINH | string | Einheit von vse_spri (Istwert Einlasspreizung Vanos) |
| STAT_VSESPRI2_WERT | real | Wert von vse2spri (Istwert Einlasspreizung Vanos 2) |
| STAT_VSESPRI2_EINH | string | Einheit von vse2spri (Istwert Einlasspreizung Vanos 2) |
| STAT_VSATV_WERT | real | Wert von vsa_tv (Tastverhältnis Auslasspreizung Vanos) |
| STAT_VSATV_EINH | string | Einheit von vsa_tv (Tastverhältnis Auslasspreizung Vanos) |
| STAT_VSATV2_WERT | real | Wert von vsa2tv (Tastverhältnis Auslasspreizung Vanos 2) |
| STAT_VSATV2_EINH | string | Einheit von vsa2tv (Tastverhältnis Auslasspreizung Vanos 2) |
| STAT_VSETV_WERT | real | Wert von vse_tv (Tastverhältnis Einlasspreizung Vanos) |
| STAT_VSETV_EINH | string | Einheit von vse_tv (Tastverhältnis Einlasspreizung Vanos) |
| STAT_VSETV2_WERT | real | Wert von vse2tv  (Tastverhältnis Einlasspreizung Vanos 2) |
| STAT_VSETV2_EINH | string | Einheit von vse2tv  (Tastverhältnis Einlasspreizung Vanos 2) |
| STAT_TAML_WERT | real | Wert von taml (Tastverhältnis E-Lüfter) |
| STAT_TAML_EINH | string | Einheit von taml (Tastverhältnis E-Lüfter) |
| STAT_KOE_EIN | int | Bedingung für Kompressor Einschalten (B_koe) |
| STAT_HSVE_EIN | int | Bedingung Heizung LS vor Kat ein (B_hsve) |
| STAT_HSVE2_EIN | int | Bedingung Heizung LS vor Kat Bank 2 ein (B_hsve) |
| STAT_HSHE_EIN | int | Bedingung Heizung LS hinter Kat ein (B_hshe) |
| STAT_HSHE2_EIN | int | Bedingung Heizung LS hinter Kat Bank 2 ein (B_hshe2) |
| STAT_AKR_EIN | int | Bedingung Abgasklappe ein (B_akr) |
| STAT_EBL_EIN | int | Bedingung E-Box Luefter ein (B_ebl) |
| STAT_EKP_EIN | int | Bedingung EKP ein (B_ekp) |
| STAT_ETR_EIN | int | Bedingung Kennfeldthermostat ein (B_etr) |
| STAT_STA_EIN | int | Bedingung Startrelais ein (B_sta) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nockenwelle-adaption"></a>
### STATUS_NOCKENWELLE_ADAPTION

0x224006 STATUS_NOCKENWELLE_ADAPTION Auslesen der NWG-Adaptionen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_VSAADP_WERT | real | Wert von vsa_adp (Adap.wert Anschlag Ausslasspreizung variable NWS) |
| STAT_VSAADP_EINH | string | Einheit von vsa_adp (Adap.wert Anschlag Ausslasspreizung variable NWS) |
| STAT_VSAADP2_WERT | real | Wert von vsa2adp (Adap.wert Anschlag Ausslasspreizung variable NWS 2) |
| STAT_VSAADP2_EINH | string | Einheit von vsa2adp (Adap.wert Anschlag Ausslasspreizung variable NWS 2) |
| STAT_VSEADP_WERT | real | Wert von vse_adp (Adap.wert Anschlag Einlasspreizung variable NWS) |
| STAT_VSEADP_EINH | string | Einheit von vse_adp (Adap.wert Anschlag Einlasspreizung variable NWS) |
| STAT_VSEADP2_WERT | real | Wert von vse2adp (Adap.wert Anschlag Einlasspreizung variable NWS 2) |
| STAT_VSEADP2_EINH | string | Einheit von vse2adp (Adap.wert Anschlag Einlasspreizung variable NWS 2) |
| STAT_VSAADPFL0_WERT | real | Wert von vsa_adp_fl |
| STAT_VSAADPFL0_EINH | string | Einheit von vsa_adp_fl0 |
| STAT_VSAADPFL1_WERT | real | Wert von vsa_adp_fl1 |
| STAT_VSAADPFL1_EINH | string | Einheit von vsa_adp_fl1 |
| STAT_VSAADPFL2_WERT | real | Wert von vsa_adp_fl2 |
| STAT_VSAADPFL2_EINH | string | Einheit von vsa_adp_fl2 |
| STAT_VSAADPFL3_WERT | real | Wert von vsa_adp_fl3 |
| STAT_VSAADPFL3_EINH | string | Einheit von vsa_adp_fl3 |
| STAT_VSAADP2FL0_WERT | real | Wert von vsa2adp_fl[0] |
| STAT_VSAADP2FL0_EINH | string | Einheit von vsa2adp_fl[0] |
| STAT_VSAADP2FL1_WERT | real | Wert von vsa2adp_fl[1] |
| STAT_VSAADP2FL1_EINH | string | Einheit von vsa2adp_fl[1] |
| STAT_VSAADP2FL2_WERT | real | Wert von vsa2adp_fl[2] |
| STAT_VSAADP2FL2_EINH | string | Einheit von vsa2adp_fl[2] |
| STAT_VSAADP2FL3_WERT | real | Wert von vsa2adp_fl[3] |
| STAT_VSAADP2FL3_EINH | string | Einheit von vsa2adp_fl_[3] |
| STAT_VSEADPFL0_WERT | real | Wert von vse_adp_fl_[0] |
| STAT_VSEADPFL0_EINH | string | Einheit von vse_adp_fl_[0] |
| STAT_VSEADPFL1_WERT | real | Wert von vse_adp_fl_[1] |
| STAT_VSEADPFL1_EINH | string | Einheit von vse_adp_fl_[1] |
| STAT_VSEADPFL2_WERT | real | Wert von vse_adp_fl_[2] |
| STAT_VSEADPFL2_EINH | string | Einheit von vse_adp_fl_[2] |
| STAT_VSEADPFL3_WERT | real | Wert von vse_adp_fl_[3] |
| STAT_VSEADPFL3_EINH | string | Einheit von vse_adp_fl_[3] |
| STAT_VSEADP2FL0_WERT | real | Wert von vse2_adp_fl0 |
| STAT_VSEADP2FL0_EINH | string | Einheit von vse2_adp_fl0 |
| STAT_VSEADP2FL1_WERT | real | Wert von vse2_adp_fl1 |
| STAT_VSEADP2FL1_EINH | string | Einheit von vse2_adp_fl1 |
| STAT_VSEADP2FL2_WERT | real | Wert von vse2_adp_fl2 |
| STAT_VSEADP2FL2_EINH | string | Einheit von vse2_adp_fl2 |
| STAT_VSEADP2FL3_WERT | real | Wert von vse2_adp_fl3 |
| STAT_VSEADP2FL3_EINH | string | Einheit von vse2_adp_fl3 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config"></a>
### ECU_CONFIG

0x30A801 ECU_CONFIG Auslesen der Variante Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DISA_GESCH_EIN | int | DISA geschaltet gelernt |
| STAT_DISA_GEREG_EIN | int | DISA 2-stufig gelernt |
| STAT_ANSKL_EIN | int | Ansaugklappe gelernt |
| STAT_AGR_EIN | int | Abgasrueckfuehrung gelernt |
| STAT_ABGK_MONO_EIN | int | Abgaskonzept Mono gelernt |
| STAT_ABGK_Y_EIN | int | Abgaskonzept Y gelernt |
| STAT_ABGK_STER_EIN | int | Abgaskonzept Stereo gelernt |
| STAT_NOKATFZ_EIN | int | Abgaskonzept ohne KAT gelernt |
| STAT_LIN_LSVK_EIN | int | Lineare Lambdasonden vor KAT gelernt |
| STAT_ZWP_LSVK_EIN | int | Zweipunkt Lambdasonden vor KAT gelernt |
| STAT_AKRFZ_EIN | int | Abgasklappe gelernt |
| STAT_SOUNDKL_EIN | int | Soundklappe gelernt |
| STAT_GLFVAR_EIN | int | Kuehler Jalousie gelernt |
| STAT_ELUE400_EIN | int | E-Luefter mit 400W gelernt |
| STAT_ELUE600_EIN | int | E-Luefter mit 600W gelernt |
| STAT_EBLVAR_EIN | int | E-Boxluefter gelernt |
| STAT_MFL_EIN | int | Multifunktionslenkrad gelernt |
| STAT_SPTVAR_EIN | int | Sporttaster gelernt |
| STAT_STRVAR_EIN | int | Starter Realais gelernt |
| STAT_TOENSVAR_EIN | int | Thermischer Oelnivausensor gelernt |
| STAT_AKKS_EIN | int | Aktive Kühlluftklappe gelernt |
| STAT_PKKS_EIN | int | Pasive Kühlluftklappe gelernt |
| STAT_HS_EIN | int | Handschalter gelernt |
| STAT_SSG_EIN | int | SSG gelernt |
| STAT_EGS_EIN | int | EGS gelernt |
| STAT_TXUGET_EIN | int | TUX Allrad gelernt |
| STAT_ASCPKW_EIN | int | Automatic Stability Control gelernt |
| STAT_ACC_EIN | int | Automatic Curise Control gelernt |
| STAT_ARSVAR_EIN | int | Dynamic Curise Control |
| STAT_AFSVAR_EIN | int | Active Front Steering gelernt |
| STAT_KOVAR_EIN | int | Relais Klimakompressor gelernt |
| STAT_IBSDETEC_EIN | int | Intelligenter Batteriesensor gelernt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config-reset"></a>
### ECU_CONFIG_RESET

0x30A804 ECU_CONFIG_RESET Loeschen der Varianten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VARIANTE_LOESCHEN | string | Gibt bei OKAY an, ob loeschen erfolgreich war |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kva"></a>
### STATUS_KVA

0x21C1 STATUS_KVA Auslesen Faktor KVA Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KVA_WERT | real | Wert von kva_korr (-0.128 ... 0.127) |
| STAT_KVA_EINH | string | Einheit von kva_korr [%] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

0x3BC100 STEUERN_KVA Korrekturfaktor Kraftstoffverbrauch kva_korr programmieren Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA_WERT | int | Wertebereich Übergabeparameter: -128 ... 127 kva_korr = KVA_WERT \ 1000 zB: KVA_WERT = -55   =&gt; kva_korr = -0.055% |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-readiness"></a>
### STATUS_READINESS

0x2105 STATUS_READINESS Auslesen des Readinessbyte Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KATFZ_EIN | int | Bedingung KatFahrzeug ein |
| STAT_CDTES_EIN | int | Bedingung Diagnosefreigabe Tankentlueftungssystem |
| STAT_CDLSV_EIN | int | Bedingung Diagnosefreigabe Lambdasonde vor Kat |
| STAT_CDHSV_EIN | int | Bedingung Diagnosefreigabe Lambdasondenheizung hinter Kat |
| STAT_CDAGR_EIN | int | Bedingung Diagnosefreigabe Abgasrueckfuehrung (nur BDE!) |
| STAT_CDSLS_EIN | int | Bedingung Diagnosefreigabe Sekundärluftsystem (nur BDE!) |
| STAT_KATRDY_EIN | int | Bedingung Katdiagnose ready |
| STAT_TESRDY_EIN | int | Bedingung Tankentlueftungssystem ready |
| STAT_LSRDY_EIN | int | Bedingung Lambdasonden ready |
| STAT_HSRDY_EIN | int | Bedingung Heizung Lambdasonden ready |
| STAT_AGRRDY_EIN | int | Bedingung Abgasrueckfuehrung ready |
| STAT_SLSRDY_EIN | int | Bedingung Sekundärluftsystem ready |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fgr"></a>
### STATUS_FGR

0x2107 STATUS_FGR Auslesen der FGR-Stati Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_FGRAT_EIN | int | Bedingung FGR Austaste ein |
| STAT_FGRHSA_EIN | int | Bedingung FGR Hauptschalter |
| STAT_FGRTBE_EIN | int | Bedingung Taste Beschleunigung |
| STAT_FGRTSE_EIN | int | Bedingung Taste Setzen |
| STAT_FGRTVE_EIN | int | Bedingung Taste Verzoegern |
| STAT_FGRTWA_EIN | int | Bedingung Taste Wiederaufnahme |
| STAT_LFGR_EIN | int | Bedingung FGR-Lampe |
| STAT_ACC_EIN | int | Bedingung ACC |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ll-abgleich"></a>
### STEUERN_LL_ABGLEICH

0x30A107 STEUERN_LL_ABGLEICH Abgleichwert LL (Leerlauf) vorgeben Aktivierung: Klemme 15 = EIN UND Leerlauf = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DNLLMV_WERT | long | Abgleichswert LL DNLLMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNSACMV_WERT | long | Abgleichswert LL mit Klimaanlage DNSACMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNSLBV_WERT | long | Abgleichswert LL mit niedriger Batteriespannung DNSLBV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNFSACMV_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung DNFSACMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNFSMV_WERT | long | Abgleichswert LL mit Fahrstufe DNFSMV   Einheit: 1/min   Min: -128 Max: 127 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

0x30A108 STEUERN_LLABG_PROG Abgleichwert LL (Leerlauf) programmieren Aktivierung: Klemme 15 = EIN UND Leerlauf = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DNLLMV_WERT | long | Abgleichswert LL DNLLMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNSACMV_WERT | long | Abgleichswert LL mit Klimaanlage DNSACMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNSLBV_WERT | long | Abgleichswert LL mit niedriger Batteriespannung DNSLBV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNFSACMV_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung DNFSACMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNFSMV_WERT | long | Abgleichswert LL mit Fahrstufe DNFSMV   Einheit: 1/min   Min: -128 Max: 127 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ll-abgleich"></a>
### STATUS_LL_ABGLEICH

0x225FF0 STATUS_LL_ABGLEICH Abgleichwert LL (Leerlauf) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DNLLMV_WERT | real | Abgleichswert LL DNLLMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNLLMV_EINH | string | 1/min |
| STAT_DNSACMV_WERT | real | Abgleichswert LL mit Klimaanlage DNSACMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNSACMV_EINH | string | 1/min |
| STAT_DNSLBV_WERT | real | Abgleichswert LL mit niedriger Batteriespannung DNSLBV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNSLBV_EINH | string | 1/min |
| STAT_DNFSACMV_WERT | real | Abgleichswert LL mit Klima und Fahrbedingung DNFSACMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNFSACMV_EINH | string | 1/min |
| STAT_DNFSMV_WERT | real | Abgleichswert LL mit Fahrstufe DNFSMV   Einheit: 1/min   Min: -128 Max: 127 |
| STAT_DNFSMV_EINH | string | 1/min |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lrp"></a>
### STATUS_LRP

0x30F601 STATUS_LRP Auslesen Funktionseingriffe bei der Laufruheprüfung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_HUBEINGRIFF_INAKTIV | int | zyl.selektiver Hubeingriff (1=deaktiviert, 0=aktiviert) |
| STAT_MINHUBEINGRIFF_INAKTIV | int | Minhubeingriff (1=deaktiviert, 0=aktiviert) |
| STAT_ZUENDWINKELEINGRIFF_INAKTIV | int | Zuendwinkeleingriff (1=deaktiviert, 0=aktiviert) |
| STAT_GEMISCHEINGRIFF_INAKTIV | int | Gemischeingriff (1=deaktiviert, 0=aktiviert) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lrp"></a>
### STEUERN_LRP

0x30F607 STEUERN_LRP Funktionseingriffe für die Laufruheprüfung vorgeben Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HUBEINGRIFF_INAKTIV | int | zyl.selektiver Hubeingriff (1=deaktiviert, 0=aktiviert) |
| MINHUBEINGRIFF_INAKTIV | int | Minhubeingriff (1=deaktiviert, 0=aktiviert) |
| ZUENDWINKELEINGRIFF_INAKTIV | int | Zuendwinkeleingriff (1=deaktiviert, 0=aktiviert) |
| GEMISCHEINGRIFF_INAKTIV | int | Gemischeingriff (1=deaktiviert, 0=aktiviert) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lrp-aus"></a>
### STEUERN_LRP_AUS

0x30F600 STEUERN_LRP_AUS Vorgabe Funktionseingriffe für die Laufruheprüfung stoppen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-lrp"></a>
### STEUERN_PROGRAMM_LRP

0x30F608 STEUERN_PROGRAMM_LRP Prüfeingriffe für die Laufruheprüfung programmieren Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HUBEINGRIFF_INAKTIV | int | zyl.selektiver Hubeingriff (1=deaktiviert, 0=aktiviert) |
| MINHUBEINGRIFF_INAKTIV | int | Minhubeingriff (1=deaktiviert, 0=aktiviert) |
| ZUENDWINKELEINGRIFF_INAKTIV | int | Zuendwinkeleingriff (1=deaktiviert, 0=aktiviert) |
| GEMISCHEINGRIFF_INAKTIV | int | Gemischeingriff (1=deaktiviert, 0=aktiviert) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-lrp"></a>
### STATUS_MESSWERTE_LRP

0x22402D STATUS_MESSWERTE_LRP Ausgelesen der Messwerte Laufruheprüfung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ST_VBRVS_AUS | unsigned long | Statuswort Verbrennungsregelung f. Service (St_vbrvs_aus) |
| STAT_ST_VBRVS_EIN | unsigned long | Statuswort Verbrennungsregelung vom Tester (St_vbrvs_ein) |
| STAT_ST_VBRVS_EINNV | unsigned long | Statuswort Verbrennungsregelung vom Tester nicht flüchtig (St_vbrvs_einnv) |
| STAT_AMO_05_WERT | real | Gesamte DFT 0,5 Motorordnung (Amo_05) |
| STAT_AMO_10_WERT | real | Gesamte DFT 1,0 Motorordnung (Amo_10) |
| STAT_AMO_15_WERT | real | Gesamte DFT 1,5 Motorordnung (Amo_15) |
| STAT_AMO_20_WERT | real | Gesamte DFT 2,0 Motorordnung (Amo_20) |
| STAT_EXWINKKOR_WERT | real | Korrekturwinkel Excenterwelle zur Hubkorrektur (Exwinkkor) |
| STAT_EXWINKKOR_EINH | string | Einheit exwinkkor: [°] |
| STAT_ZYLHUBKOR | unsigned long | Für Hubkorrektur ausgewählter Zylinder (zylhubkor) |
| STAT_MNHUB_WERT | real | Tatsächlich wirksamer Minhub (Minhub) |
| STAT_MNHUB_EINH | string | Einheit minhub: [mm] |
| STAT_F_MNHUB_WERT | real | Faktor Ein-/ Ausblendung Minhub über tmot u. nkw (F_minhub) |
| STAT_MNHUB_ROH_WERT | real | Minhubrohwert aus Adaption (Minhub_roh) |
| STAT_MNHUB_ROH_EINH | string | Einheit Minhub_roh: [mm] |
| STAT_MNHUBVS_WERT | real | Vorgabe Minhub über Tester (Minhubvs) |
| STAT_MNHUBVS_EINH | string | Einheit Minhubvs: [mm] |
| STAT_MNHUBVS_IST_WERT | real | Tatsächlich wirksamer minhub aus Verstelleingriff (Minhubvs_ist) |
| STAT_MNHUBVS_IST_EINH | string | Einheit Minhubvs_ist: [mm] |
| STAT_MNHUBVSNV_WERT | real | Dauerhaft fest programmierter Minhub (Minhubvsnv) |
| STAT_MNHUBVSNV_EINH | string | Einheit Minhubvsnv: [mm] |
| STAT_S_VSMNHB | unsigned long | Schalter für Testereingriff (S_vsmnhb) |
| STAT_S_VSMNHBNV | unsigned long | Schalter für Testereingriff (S_vsmnhbnv) |
| STAT_F_TIKORRVR_0_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_0_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_0_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_0_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_0_EINH | string | Einheit Zw_offkorrvr: [°] |
| STAT_F_TIKORRVR_1_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_1_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_1_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_1_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_1_EINH | string | Einheit Zw_offkorrvr: [°] |
| STAT_F_TIKORRVR_2_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_2_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_2_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_2_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_2_EINH | string | Einheit Zw_offkorrvr: [°] |
| STAT_F_TIKORRVR_3_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_3_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_3_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_3_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_3_EINH | string | Einheit Zw_offkorrvr: [°] |
| STAT_F_TIKORRVR_4_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_4_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_4_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_4_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_4_EINH | string | Einheit Zw_offkorrvr: [°] |
| STAT_F_TIKORRVR_5_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_5_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_5_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_5_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_5_EINH | string | Einheit Zw_offkorrvr: [°] |
| STAT_F_TIKORRVR_6_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_6_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_6_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_6_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_6_EINH | string | Einheit Zw_offkorrvr: [°] |
| STAT_F_TIKORRVR_7_WERT | real | Zylinderselektive Gemischkorrektur (F_tikorrvr) |
| STAT_LURABS_F_7_WERT | real | Gefilterte Laufunruhedeltas eines Zylinders (Lurabs_f) |
| STAT_LURDIF_F_7_WERT | real | Gefilterte mittlere Abweichung des Lur-Wertes (Lurdif_f) |
| STAT_ZW_OFFKORRVR_7_WERT | real | Zündwinkeloffset für Verbrennungsregelung (Zw_offkorrvr) |
| STAT_ZW_OFFKORRVR_7_EINH | string | Einheit Zw_offkorrvr: [°] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-vvt"></a>
### STATUS_MESSWERTE_VVT

0x22400B STATUS_MESSWERTE_VVT VVT Messwerte auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_VVTSW_WERT | real | Wert von vvt_sw (VVT-Sollwert Bank 1) |
| STAT_VVTSW_EINH | string | Einheit von vvt_sw (VVT-Sollwert Bank 1) |
| STAT_VVTIW_WERT | real | Wert von vvt_iw (VVT-Istwert Bank 1) |
| STAT_VVTIW_EINH | string | Einheit von vvt_iw (VVT-Istwert Bank 1) |
| STAT_VVTTV_WERT | real | Wert von vvt_tv (VVT-Tastverhältnis Bank 1) |
| STAT_VVTTV_EINH | string | Einheit von vvt_tv (VVT-Tastverhältnis Bank 1) |
| STAT_VVTES_WERT | real | Wert von vvt_es (VVT-Strombedarf Bank 1) |
| STAT_VVTES_EINH | string | Einheit von vvt_es (VVT-Strombedarf Bank 1) |
| STAT_VVTSW2_WERT | real | Wert von vvt_sw2 (VVT-Sollwert Bank 2) |
| STAT_VVTSW2_EINH | string | Einheit von vvt_sw2 (VVT-Sollwert Bank 2) |
| STAT_VVTIW2_WERT | real | Wert von vvt_iw2 (VVT-Istwert Bank 2) |
| STAT_VVTIW2_EINH | string | Einheit von vvt_iw2 (VVT-Istwert Bank 2) |
| STAT_VVTTV2_WERT | real | Wert von vvt_tv2 (VVT-Tastverhältnis Bank 2) |
| STAT_VVTTV2_EINH | string | Einheit von vvt_tv2 (VVT-Tastverhältnis Bank 2) |
| STAT_VVTES2_WERT | real | Wert von vvt_es2 (VVT-Strombedarf Bank 2) |
| STAT_VVTES2_EINH | string | Einheit von vvt_es2 (VVT-Strombedarf Bank 2) |
| STAT_MINHUBVSI_WERT | real | Wert von minhubvsi (ü. Tester vorgegeb. Minhub) |
| STAT_MINHUBVSI_EINH | string | Einheit von minhubvsi (ü. Tester vorgegeb. Minhub) |
| STAT_DELTAGVFI_WERT | real | Wert von deltagvfi (deltagvf nach PT1-Filter) |
| STAT_DELTAGVFI_EINH | string | Einheit von deltagvfi (deltagvf nach PT1-Filter) |
| STAT_FLUB1_WERT | real | Wert von flub1_w (Mittelwert Laufunruhe gefiltert Bank 1) |
| STAT_FLUB1_EINH | string | Einheit von flub1_w (Mittelwert Laufunruhe gefiltert Bank 1) |
| STAT_FLUB2_WERT | real | Wert von flub2_w (Mittelwert Laufunruhe gefiltert Bank 2) |
| STAT_FLUB2_EINH | string | Einheit von flub2_w (Mittelwert Laufunruhe gefiltert Bank 2) |
| STAT_MINHUBROH_WERT | real | Wert von minhub_roh (Minhub v. Tester oder aus Adaption) |
| STAT_MINHUBROH_EINH | string | Einheit von minhub_roh (Minhub v. Tester oder aus Adaption) |
| STAT_NMOT_EIN | int | Wert von B_nmot (Bed. Motordrehzahl: n&gt;NMIN) |
| STAT_MINHUBVS_EIN | int | Wert von B_minhubvs (Bed. Adaptionswerte werden gelöscht) |
| STAT_FBGL_EIN | int | Wert von B_fbgl (Bed. Freigabe Bankabgleich) |
| STAT_BGL_EIN | int | Wert von B_bgl (Bed. Bankabgleich aktiv) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta1"></a>
### STATUS_FASTA1

0x22400C STATUS_FASTA1 Auslesen FASTA-Messwertblock 1 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TSG_WERT | real | Wert von tsg |
| STAT_TSG_EINH | string | Einheit von tsg |
| STAT_KRDWS_EIN | int | Wert von B_krdws |
| STAT_DMVAD_WERT | real | Wert von dmvad_w |
| STAT_DMVAD_EINH | string | Einheit von dmvad_w |
| STAT_DPS_WERT | real | Wert von dps_w |
| STAT_DPS_EINH | string | Einheit von dps_w |
| STAT_DPSRAUS_WERT | real | Wert von dpsraus_i |
| STAT_DPSRAUS_EINH | string | Einheit von dpsraus_i |
| STAT_FKMSVVT_WERT | real | Wert von fkmsvvt_w |
| STAT_FKMSVVT_EINH | string | Einheit von fkmsvvt_w |
| STAT_FPRSTEP_WERT | real | Wert von fprstep_c |
| STAT_FPRSTEP_EINH | string | Einheit von fprstep_c |
| STAT_LRNSTEP_WERT | real | Wert von lrnstep_c |
| STAT_LRNSTEP_EINH | string | Einheit von lrnstep_c |
| STAT_MSNVVTO_WERT | real | Wert von msnvvto_w |
| STAT_MSNVVTO_EINH | string | Einheit von msnvvto_w |
| STAT_NNW10_WERT | real | Wert von nn_w1_0 |
| STAT_NNW10_EINH | string | Einheit von nn_w1_0 |
| STAT_NNW11_WERT | real | Wert von nn_w1_1 |
| STAT_NNW11_EINH | string | Einheit von nn_w1_1 |
| STAT_NNW12_WERT | real | Wert von nn_w1_2 |
| STAT_NNW12_EINH | string | Einheit von nn_w1_2 |
| STAT_NNW20_WERT | real | Wert von nn_w2_0 |
| STAT_NNW20_EINH | string | Einheit von nn_w2_0 |
| STAT_NNW21_WERT | real | Wert von nn_w2_1 |
| STAT_NNW21_EINH | string | Einheit von nn_w2_1 |
| STAT_NNW22_WERT | real | Wert von nn_w2_2 |
| STAT_NNW22_EINH | string | Einheit von nn_w2_2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta2"></a>
### STATUS_FASTA2

0x22400D STATUS_FASTA2 Auslesen FASTA-Messwertblock 2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_NSOLFASTA_WERT | real | Wert von nsol_w |
| STAT_NSOLFASTA_EINH | string | Einheit von nsol_w |
| STAT_RL_WERT | real | Wert von rl_w |
| STAT_RL_EINH | string | Einheit von rl_w |
| STAT_RLSOL_WERT | real | Wert von rlsol_w |
| STAT_RLSOL_EINH | string | Einheit von rlsol_w |
| STAT_TE_WERT | real | Wert von te_w |
| STAT_TE_EINH | string | Einheit von te_w |
| STAT_TE2_WERT | real | Wert von te2_w |
| STAT_TE2_EINH | string | Einheit von te2_w |
| STAT_VVTSTATUS_WERT | real | Wert von vvtstatus |
| STAT_VVTSTATUS_EINH | string | Einheit von vvtstatus |
| STAT_WDKBAFASTA_WERT | real | Wert von wdkba_w |
| STAT_WDKBAFASTA_EINH | string | Einheit von wdkba_w |
| STAT_WDKS_WERT | real | Wert von wdks_w |
| STAT_WDKS_EINH | string | Einheit von wdks_w |
| STAT_WPED_WERT | real | Wert von wped_w |
| STAT_WPED_EINH | string | Einheit von wped_w |
| STAT_ZWIST_WERT | real | Wert von zwist |
| STAT_ZWIST_EINH | string | Einheit von zwist |
| STAT_MIL_EIN | int | Wert von B_mil |
| STAT_DMLLRI_WERT | real | Wert von dmllri_w |
| STAT_DMLLRI_EINH | string | Einheit von dmllri_w |
| STAT_MIMIN_WERT | real | Wert von mimin_w |
| STAT_MIMIN_EINH | string | Einheit von mimin_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta3"></a>
### STATUS_FASTA3

0x22400E STATUS_FASTA3 Auslesen FASTA-Messwertblock 3 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MDGEN_WERT | real | Wert von mdgen |
| STAT_MDGEN_EINH | string | Einheit von mdgen |
| STAT_MDKO_WERT | real | Wert von mdko |
| STAT_MDKO_EINH | string | Einheit von mdko |
| STAT_DMRLLR_WERT | real | Wert von dmrllr_w |
| STAT_DMRLLR_EINH | string | Einheit von dmrllr_w |
| STAT_FS_EIN | int | Wert von B_fs |
| STAT_MDWAN_WERT | real | Wert von mdwan ist eigentlich eine Word-Groesse |
| STAT_MDWAN_EINH | string | Einheit von mdwan |
| STAT_DWKR_WERT | real | Wert von dwkr |
| STAT_DWKR_EINH | string | Einheit von dwkr |
| STAT_DZWS_WERT | real | Wert von dzws |
| STAT_DZWS_EINH | string | Einheit von dzws |
| STAT_DFFGEN_WERT | real | Wert von dffgen |
| STAT_DFFGEN_EINH | string | Einheit von dffgen |
| STAT_TUMG_WERT | real | Wert von tumg |
| STAT_TUMG_EINH | string | Einheit von tumg |
| STAT_DMVADFS_WERT | real | Wert von dmvadfs |
| STAT_DMVADFS_EINH | string | Einheit von dmvadfs |
| STAT_DMVADKO_WERT | real | Wert von dmvadko |
| STAT_DMVADKO_EINH | string | Einheit von dmvadko |
| STAT_DLAHI_WERT | real | Wert von dlahi_w |
| STAT_DLAHI_EINH | string | Einheit von dlahi_w |
| STAT_DLAHI2_WERT | real | Wert von dlahi2_w |
| STAT_DLAHI2_EINH | string | Einheit von dlahi2_w |
| STAT_RINH_WERT | real | Wert von rinh_w |
| STAT_RINH_EINH | string | Einheit von rinh_w |
| STAT_RINH2_WERT | real | Wert von rinh2_w |
| STAT_RINH2_EINH | string | Einheit von rinh2_w |
| STAT_RKATS_WERT | real | Wert von rkats_w |
| STAT_RKATS_EINH | string | Einheit von rkats_w |
| STAT_DPSSOL_WERT | real | Wert von dpssol_w |
| STAT_DPSSOL_EINH | string | Einheit von dpssol_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta4"></a>
### STATUS_FASTA4

0x22400F STATUS_FASTA4 Auslesen FASTA-Messwertblock 4 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ECULOCK_EIN | int | Wert von B_eculock |
| STAT_LRNRDY_EIN | int | Wert von B_lrnrdy |
| STAT_LLTD_EIN | int | Wert von B_lltd |
| STAT_LLK_EIN | int | Wert von B_llk |
| STAT_TEAKT_EIN | int | Wert von B_teakt |
| STAT_VVTNOTL_EIN | int | Wert von B_vvtnotl |
| STAT_NVRBUPOK_EIN | int | Wert von B_nvrbupok --&gt; Rambackup ok |
| STAT_COPOT_WERT | real | Wert von co_pot_w |
| STAT_COPOT_EINH | string | Einheit von co_pot_w |
| STAT_UPWG_WERT | real | Wert von upwg_w |
| STAT_UPWG_EINH | string | Einheit von upwg_w |
| STAT_MINHUB_WERT | real | Wert von minhub_w |
| STAT_MINHUB_EINH | string | Einheit von minhub_w |
| STAT_GVIST_WERT | real | Wert von gvist |
| STAT_GVIST_EINH | string | Einheit von gvist |
| STAT_FTBR_WERT | real | Wert von ftbr_w |
| STAT_FTBR_EINH | string | Einheit von ftbr_w |
| STAT_FHO_WERT | real | Wert von fho_w |
| STAT_FHO_EINH | string | Einheit von fho_w |
| STAT_FTVDK_WERT | real | Wert von ftvdk |
| STAT_FTVDK_EINH | string | Einheit von ftvdk |
| STAT_MSNVVTOLL_WERT | real | Wert von msnvvtoll_w |
| STAT_MSNVVTOLL_EINH | string | Einheit von msnvvtoll_w |
| STAT_VSESPRS_WERT | real | Wert von vse_sprs |
| STAT_VSESPRS_EINH | string | Einheit von vse_sprs |
| STAT_VSE2SPRS_WERT | real | Wert von vse2sprs |
| STAT_VSE2SPRS_EINH | string | Einheit von vse2sprs |
| STAT_VSASPRS_WERT | real | Wert von vsa_sprs |
| STAT_VSASPRS_EINH | string | Einheit von vsa_sprs |
| STAT_VSA2SPRS_WERT | real | Wert von vsa2sprs |
| STAT_VSA2SPRS_EINH | string | Einheit von vsa2sprs |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta5"></a>
### STATUS_FASTA5

0x224010 STATUS_FASTA5 Auslesen FASTA-Messwertblock 5 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ATMTPA_EIN | int | Wert von B_atmtpa |
| STAT_ATMTPK_EIN | int | Wert von B_atmtpk |
| STAT_EVHUBI_WERT | real | Wert von evhubi_w |
| STAT_EVHUBI_EINH | string | Einheit von evhubi_w |
| STAT_EVHUBI2_WERT | real | Wert von evhubi2_w |
| STAT_EVHUBI2_EINH | string | Einheit von evhubi2_w |
| STAT_EVHUBS_WERT | real | Wert von evhubs_w |
| STAT_EVHUBS_EINH | string | Einheit von evhubs_w |
| STAT_OFWNKADBG_WERT | real | Wert von ofwnkadbg |
| STAT_OFWNKADBG_EINH | string | Einheit von ofwnkadbg |
| STAT_KH_EIN | int | Wert von B_kh |
| STAT_NSUB_EIN | int | Wert von B_nsub |
| STAT_TE_EIN | int | Wert von B_te |
| STAT_DFSERESZ_WERT | real | Wert von dfseresz_w |
| STAT_DFSERESZ_EINH | string | Einheit von dfseresz_w |
| STAT_DMVADFK_WERT | real | Wert von dmvadfk_w |
| STAT_DMVADFK_EINH | string | Einheit von dmvadfk_w |
| STAT_DMVADLL_WERT | real | Wert von dmvadll_w |
| STAT_DMVADLL_EINH | string | Einheit von dmvadll_w |
| STAT_EXWINKI_WERT | real | Wert von exwinki_w |
| STAT_EXWINKI_EINH | string | Einheit von exwinki_w |
| STAT_EXWINKI2_WERT | real | Wert von exwinki2_w |
| STAT_EXWINKI2_EINH | string | Einheit von exwinki2_w |
| STAT_EXWINKS_WERT | real | Wert von exwinks_w |
| STAT_EXWINKS_EINH | string | Einheit von exwinks_w |
| STAT_FE_WERT | int | Wert von B_fe (ist kein Flag!) |
| STAT_FE_EINH | string | Einheit von B_fe |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta6"></a>
### STATUS_FASTA6

0x224011 STATUS_FASTA6 Auslesen FASTA-Messwertblock 6 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_FKMSVVTA_WERT | real | Wert von fkmsvvta_w |
| STAT_FKMSVVTA_EINH | string | Einheit von fkmsvvta_w |
| STAT_FOFRESZ_WERT | real | Wert von fofresz |
| STAT_FOFRESZ_EINH | string | Einheit von fofresz |
| STAT_MSDIF_WERT | real | Wert von msdif_w |
| STAT_MSDIF_EINH | string | Einheit von msdif_w |
| STAT_TABGM_WERT | real | Wert von tabgm |
| STAT_TABGM_EINH | string | Einheit von tabgm |
| STAT_TNSE_WERT | real | Wert von tnse_w |
| STAT_TNSE_EINH | string | Einheit von tnse_w |
| STAT_OZRWPERM_WERT | real | Wert von ozrwperm |
| STAT_OZRWPERM_EINH | string | Einheit von ozrwperm |
| STAT_OZRWKVB_WERT | real | Wert von ozrwkvb |
| STAT_OZRWKVB_EINH | string | Einheit von ozrwkvb |
| STAT_OZOELZEIT_WERT | real | Wert von ozoelzeit |
| STAT_OZOELZEIT_EINH | string | Einheit von ozoelzeit |
| STAT_OZKVBSM_WERT | real | Wert von ozkvbsm_ul |
| STAT_OZKVBSM_EINH | string | Einheit von ozkvbsm_ul |
| STAT_OZPERMLOW_WERT | real | Wert von ozpermlow |
| STAT_OZPERMLOW_EINH | string | Einheit von ozpermlow |
| STAT_OZPERMEX_WERT | real | Wert von ozpermex |
| STAT_OZPERMEX_EINH | string | Einheit von ozpermex |
| STAT_OZPERMOFF_WERT | real | Wert von ozpermoff |
| STAT_OZPERMOFF_EINH | string | Einheit von ozpermoff |
| STAT_OZKVBOG_WERT | real | Wert von ozkvbog |
| STAT_OZKVBOG_EINH | string | Einheit von ozkvbog |
| STAT_OZPERMBOG_WERT | real | Wert von ozpermbog |
| STAT_OZPERMBOG_EINH | string | Einheit von ozpermbog |
| STAT_OZOELKM_WERT | real | Wert von ozoelkm |
| STAT_OZOELKM_EINH | string | Einheit von ozoelkm |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta7"></a>
### STATUS_FASTA7

0x224012 STATUS_FASTA7 Auslesen FASTA-Messwertblock 7 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_NADMTLL_WERT | real | Wert von nadmtll_w |
| STAT_NADMTLL_EINH | string | Einheit von nadmtll_w |
| STAT_NTGLM_WERT | real | Wert von ntglm_w |
| STAT_NTGLM_EINH | string | Einheit von ntglm_w |
| STAT_NTKLM_WERT | real | Wert von ntklm_w |
| STAT_NTKLM_EINH | string | Einheit von ntklm_w |
| STAT_NDIPFRO_WERT | real | Wert von ndipfro_w |
| STAT_NDIPFRO_EINH | string | Einheit von ndipfro_w |
| STAT_NKFL_WERT | real | Wert von nkfl |
| STAT_NKFL_EINH | string | Einheit von nkfl |
| STAT_SSLLCNT_WERT | real | Wert von ssllcnt |
| STAT_SSLLCNT_EINH | string | Einheit von ssllcnt |
| STAT_MINHUBFAK_WERT | real | Wert von minhubfak |
| STAT_MINHUBFAK_EINH | string | Einheit von minhubfak |
| STAT_MINADRDY_WERT | real | Wert von minadrdy |
| STAT_MINADRDY_EINH | string | Einheit von minadrdy |
| STAT_BGLFLAGS1_NR | int | Wert von bgl_flags1 |
| STAT_BGLFLAGS2_NR | int | Wert von bgl_flags2 |
| STAT_BGLFLAGS3_NR | int | Wert von bgl_flags3 |
| STAT_BGLFLAGS4_NR | int | Wert von bgl_flags4 |
| STAT_SSLL_EIN | int | Wert von B_ssll |
| STAT_TDAON_EIN | int | Wert von B_tdaon |
| STAT_BGLRDY_EIN | int | Wert von B_bglrdy |
| STAT_FDLUBBGL_WERT | real | Wert von fdlubbgl_w |
| STAT_FDLUBBGL_EINH | string | Einheit von fdlubbgl_w |
| STAT_OFWNKBG1_WERT | real | Wert von ofwnkbg1 |
| STAT_OFWNKBG1_EINH | string | Einheit von ofwnkbg1 |
| STAT_OFWNKBG2_WERT | real | Wert von ofwnkbg2 |
| STAT_OFWNKBG2_EINH | string | Einheit von ofwnkbg2 |
| STAT_OFWNKMX_WERT | real | Wert von ofwnkmx |
| STAT_OFWNKMX_EINH | string | Einheit von ofwnkmx |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta10"></a>
### STATUS_FASTA10

0x224015 STATUS_FASTA10 Auslesen FASTA-Messwertblock 10 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_BSZSIFNP | long | Wert von bszsifnp_l (Serviceintervall Betriebsstundenzähler) |
| STAT_BSZSIFNP_EINH | string | Einheit v. bszsifnp_l (Serviceintervall Betriebsstundenzähler) |
| STAT_NMDSFNP_00 | int | Wert von nmdsfnp[ 0] (Sekundärkennfeldpunkt 00) |
| STAT_NMDSFNP_01 | int | Wert von nmdsfnp[ 1] (Sekundärkennfeldpunkt 01) |
| STAT_NMDSFNP_02 | int | Wert von nmdsfnp[ 2] (Sekundärkennfeldpunkt 02) |
| STAT_NMDSFNP_03 | int | Wert von nmdsfnp[ 3] (Sekundärkennfeldpunkt 03) |
| STAT_NMDSFNP_04 | int | Wert von nmdsfnp[ 4] (Sekundärkennfeldpunkt 04) |
| STAT_NMDSFNP_05 | int | Wert von nmdsfnp[ 5] (Sekundärkennfeldpunkt 05) |
| STAT_NMDSFNP_06 | int | Wert von nmdsfnp[ 6] (Sekundärkennfeldpunkt 06) |
| STAT_NMDSFNP_07 | int | Wert von nmdsfnp[ 7] (Sekundärkennfeldpunkt 07) |
| STAT_NMDSFNP_10 | int | Wert von nmdsfnp[ 8] (Sekundärkennfeldpunkt 10) |
| STAT_NMDSFNP_11 | int | Wert von nmdsfnp[ 9] (Sekundärkennfeldpunkt 11) |
| STAT_NMDSFNP_12 | int | Wert von nmdsfnp[10] (Sekundärkennfeldpunkt 12) |
| STAT_NMDSFNP_13 | int | Wert von nmdsfnp[11] (Sekundärkennfeldpunkt 13) |
| STAT_NMDSFNP_14 | int | Wert von nmdsfnp[12] (Sekundärkennfeldpunkt 14) |
| STAT_NMDSFNP_15 | int | Wert von nmdsfnp[13] (Sekundärkennfeldpunkt 15) |
| STAT_NMDSFNP_16 | int | Wert von nmdsfnp[14] (Sekundärkennfeldpunkt 16) |
| STAT_NMDSFNP_17 | int | Wert von nmdsfnp[15] (Sekundärkennfeldpunkt 17) |
| STAT_NMDSFNP_20 | int | Wert von nmdsfnp[16] (Sekundärkennfeldpunkt 20) |
| STAT_NMDSFNP_21 | int | Wert von nmdsfnp[17] (Sekundärkennfeldpunkt 21) |
| STAT_NMDSFNP_22 | int | Wert von nmdsfnp[18] (Sekundärkennfeldpunkt 22) |
| STAT_NMDSFNP_23 | int | Wert von nmdsfnp[19] (Sekundärkennfeldpunkt 23) |
| STAT_NMDSFNP_24 | int | Wert von nmdsfnp[20] (Sekundärkennfeldpunkt 24) |
| STAT_NMDSFNP_25 | int | Wert von nmdsfnp[21] (Sekundärkennfeldpunkt 25) |
| STAT_NMDSFNP_26 | int | Wert von nmdsfnp[22] (Sekundärkennfeldpunkt 26) |
| STAT_NMDSFNP_27 | int | Wert von nmdsfnp[23] (Sekundärkennfeldpunkt 27) |
| STAT_NMDSFNP_30 | int | Wert von nmdsfnp[24] (Sekundärkennfeldpunkt 30) |
| STAT_NMDSFNP_31 | int | Wert von nmdsfnp[25] (Sekundärkennfeldpunkt 31) |
| STAT_NMDSFNP_32 | int | Wert von nmdsfnp[26] (Sekundärkennfeldpunkt 32) |
| STAT_NMDSFNP_33 | int | Wert von nmdsfnp[27] (Sekundärkennfeldpunkt 33) |
| STAT_NMDSFNP_34 | int | Wert von nmdsfnp[28] (Sekundärkennfeldpunkt 34) |
| STAT_NMDSFNP_35 | int | Wert von nmdsfnp[29] (Sekundärkennfeldpunkt 35) |
| STAT_NMDSFNP_36 | int | Wert von nmdsfnp[30] (Sekundärkennfeldpunkt 36) |
| STAT_NMDSFNP_37 | int | Wert von nmdsfnp[31] (Sekundärkennfeldpunkt 37) |
| STAT_NMDSFNP_40 | int | Wert von nmdsfnp[32] (Sekundärkennfeldpunkt 40) |
| STAT_NMDSFNP_41 | int | Wert von nmdsfnp[33] (Sekundärkennfeldpunkt 41) |
| STAT_NMDSFNP_42 | int | Wert von nmdsfnp[34] (Sekundärkennfeldpunkt 42) |
| STAT_NMDSFNP_43 | int | Wert von nmdsfnp[35] (Sekundärkennfeldpunkt 43) |
| STAT_NMDSFNP_44 | int | Wert von nmdsfnp[36] (Sekundärkennfeldpunkt 44) |
| STAT_NMDSFNP_45 | int | Wert von nmdsfnp[37] (Sekundärkennfeldpunkt 45) |
| STAT_NMDSFNP_46 | int | Wert von nmdsfnp[38] (Sekundärkennfeldpunkt 46) |
| STAT_NMDSFNP_47 | int | Wert von nmdsfnp[39] (Sekundärkennfeldpunkt 47) |
| STAT_NMDSFNP_50 | int | Wert von nmdsfnp[40] (Sekundärkennfeldpunkt 50) |
| STAT_NMDSFNP_51 | int | Wert von nmdsfnp[41] (Sekundärkennfeldpunkt 51) |
| STAT_NMDSFNP_52 | int | Wert von nmdsfnp[42] (Sekundärkennfeldpunkt 52) |
| STAT_NMDSFNP_53 | int | Wert von nmdsfnp[43] (Sekundärkennfeldpunkt 53) |
| STAT_NMDSFNP_54 | int | Wert von nmdsfnp[44] (Sekundärkennfeldpunkt 54) |
| STAT_NMDSFNP_55 | int | Wert von nmdsfnp[45] (Sekundärkennfeldpunkt 55) |
| STAT_NMDSFNP_56 | int | Wert von nmdsfnp[46] (Sekundärkennfeldpunkt 56) |
| STAT_NMDSFNP_57 | int | Wert von nmdsfnp[47] (Sekundärkennfeldpunkt 57) |
| STAT_DFDSFNP_00 | int | Wert von dfdsprofle[ 0] (Kennfeldpunkt 00) |
| STAT_DFDSFNP_01 | int | Wert von dfdsprofle[ 1] (Kennfeldpunkt 01) |
| STAT_DFDSFNP_02 | int | Wert von dfdsprofle[ 2] (Kennfeldpunkt 02) |
| STAT_DFDSFNP_03 | int | Wert von dfdsprofle[ 3] (Kennfeldpunkt 03) |
| STAT_DFDSFNP_10 | int | Wert von dfdsprofle[ 4] (Kennfeldpunkt 10) |
| STAT_DFDSFNP_11 | int | Wert von dfdsprofle[ 5] (Kennfeldpunkt 11) |
| STAT_DFDSFNP_12 | int | Wert von dfdsprofle[ 6] (Kennfeldpunkt 12) |
| STAT_DFDSFNP_13 | int | Wert von dfdsprofle[ 7] (Kennfeldpunkt 13) |
| STAT_DFDSFNP_20 | int | Wert von dfdsprofle[ 8] (Kennfeldpunkt 20) |
| STAT_DFDSFNP_21 | int | Wert von dfdsprofle[ 9] (Kennfeldpunkt 21) |
| STAT_DFDSFNP_22 | int | Wert von dfdsprofle[10] (Kennfeldpunkt 22) |
| STAT_DFDSFNP_23 | int | Wert von dfdsprofle[11] (Kennfeldpunkt 23) |
| STAT_DFDSFNP_30 | int | Wert von dfdsprofle[12] (Kennfeldpunkt 30) |
| STAT_DFDSFNP_31 | int | Wert von dfdsprofle[13] (Kennfeldpunkt 31) |
| STAT_DFDSFNP_32 | int | Wert von dfdsprofle[14] (Kennfeldpunkt 32) |
| STAT_DFDSFNP_33 | int | Wert von dfdsprofle[15] (Kennfeldpunkt 33) |
| STAT_IGENKFNP | real | Wert von igenkfnp_l (Generatorstrom kumuliert) |
| STAT_IGENKFNP_EINH | string | Einheit von igenkfnp_l (Generatorstrom kumuliert) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort an SG |

<a id="job-status-messwertblock-adc"></a>
### STATUS_MESSWERTBLOCK_ADC

0x304101 STATUS_MESSWERTBLOCK_ADC Auslesen ADC-Werte Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_WTSG_WERT | real | Wert von wtsg |
| STAT_WTSG_EINH | string | Einheit von WTSG |
| STAT_USHK2_WERT | real | Wert von ushk_2 |
| STAT_USHK2_EINH | string | Einheit von ushk_2 |
| STAT_UPWG1_WERT | real | Wert von upwg1_w |
| STAT_UPWG1_EINH | string | Einheit von upwg1_w |
| STAT_UPWG2_WERT | real | Wert von upwg2_w |
| STAT_UPWG2_EINH | string | Einheit von upwg2_w |
| STAT_USHK_WERT | real | Wert von ushk_w |
| STAT_USHK_EINH | string | Einheit von ushk_w |
| STAT_WUB_WERT | real | Wert von wub |
| STAT_WUB_EINH | string | Einheit von wub |
| STAT_UDKP2_WERT | real | Wert von udkp2_w |
| STAT_UDKP2_EINH | string | Einheit von udkp2_w |
| STAT_UDKP1V_WERT | real | Wert von udkp1v_w |
| STAT_UDKP1V_EINH | string | Einheit von udkp1v_w |
| STAT_UDKP1_WERT | real | Wert von udkp1_w |
| STAT_UDKP1_EINH | string | Einheit von udkp1_w |
| STAT_TPMSHFM_WERT | real | Wert von tpmshfm_w |
| STAT_TPMSHFM_EINH | string | Einheit von tpmshfm_w |
| STAT_WTMOT_WERT | real | Wert von wtmot |
| STAT_WTMOT_EINH | string | Einheit von wtmot |
| STAT_WTFA1_WERT | real | Wert von wtfa1 |
| STAT_WTFA1_EINH | string | Einheit von wtfa1 |
| STAT_WTKA_WERT | real | Wert von wtka |
| STAT_WTKA_EINH | string | Einheit von wtka |
| STAT_UHSV_WERT | real | Wert von uhsv |
| STAT_UHSV_EINH | string | Einheit von uhsv |
| STAT_UHSV2_WERT | real | Wert von uhsv2 |
| STAT_UHSV2_EINH | string | Einheit von uhsv2 |
| STAT_UHSH_WERT | real | Wert von uhsh |
| STAT_UHSH_EINH | string | Einheit von uhsh |
| STAT_UHSH2_WERT | real | Wert von uhsh2 |
| STAT_UHSH2_EINH | string | Einheit von uhsh2 |
| STAT_DISA_WERT | real | Wert von disa_spg |
| STAT_DISA_EINH | string | Einheit von disa_spg |
| STAT_UDDSS_WERT | real | Wert von uddss_w |
| STAT_UDDSS_EINH | string | Einheit von uddss_w |
| STAT_UDSU_WERT | real | Wert von udsu_w |
| STAT_UDSU_EINH | string | Einheit von udsu_w |
| _TEL_AUFTRAG_WTSG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTSG | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_USHK | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_USHK | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_USHK2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_USHK2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UPWG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UPWG1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UPWG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UPWG2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WUB | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WUB | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDKP1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDKP1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDKP2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDKP2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDKP1V | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDKP1V | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_TPMSHFM | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_TPMSHFM | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WTMOT | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTMOT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WTFA1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTFA1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WTKA | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTKA | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UHSV | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UHSV | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UHSV2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UHSV2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UHSH | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UHSH | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UHSH2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UHSH2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_DISA | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_DISA | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDDSS | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDDSS | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDSU | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDSU | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lsu"></a>
### START_SYSTEMCHECK_LSU

0x31E800 START_SYSTEMCHECK_LSU Systemdiagnose LSU starten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lsu"></a>
### STATUS_SYSTEMCHECK_LSU

0x2125 STATUS_SYSTEMCHECK_LSU Status Systemdiagnose LSU Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LSU_WERT | int | Status der LSU-Diagnose Bank 1 (lsunpstat) |
| STAT_LSU2_WERT | int | Status der LSU-Diagnose Bank 2 (lsunpstat2) |
| STAT_LSUBANK1_TEXT | string | Status der LSU-Diagnose Bank 1 (lsunpstat) |
| STAT_LSUBANK2_TEXT | string | Status der LSU-Diagnose Bank 2 (lsunpstat2) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lsu-neu"></a>
### STATUS_SYSTEMCHECK_LSU_NEU

0x2125 STATUS_SYSTEMCHECK_LSU_NEU Status Systemdiagnose LSU Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LSU_WERT | int | Status der LSU-Diagnose Bank 1+Bank 2 (Wert) |
| STAT_LSU_TEXT | string | comment  : Status der LSU-Diagnose Bank 1+Bank 2 (Text) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lsu"></a>
### STOP_SYSTEMCHECK_LSU

0x32E800 STOP_SYSTEMCHECK_LSU Ende Systemdiagnose LSU Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-kat"></a>
### START_SYSTEMCHECK_KAT

0x31EB00 START_SYSTEMCHECK_KAT Systemdiagnose KAT Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BANK | int | selektiert die Bank aus (1--&gt; Bank 1, 2--&gt; Bank 2, 3--&gt; Bank 1 und 2) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-kat"></a>
### STATUS_SYSTEMCHECK_KAT

0x211C STATUS_SYSTEMCHECK_KAT Status Systemtest KAT Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_KAT_WERT | int | Status der KAT-Diagnose |
| STAT_SYSTEMCHECK_KAT_TEXT | string | Status der KAT-Diagnose |
| STAT_SYSTEMCHECK_KAT2_WERT | int | Status der KAT-Diagnose |
| STAT_SYSTEMCHECK_KAT2_TEXT | string | Status der KAT-Diagnose |
| STAT_OSCDKTF_WERT | real | Wert von oscdktf_w (gefilt. Speichervermögen des KAT) |
| STAT_OSCDKTF_EINH | string | Einheit von oscdktf_w |
| STAT_OSCDKTF2_WERT | real | Wert von oscdktf2_w (gefilt. Speichervermögen des KAT) |
| STAT_OSCDKTF2_EINH | string | Einheit von oscdktf2_w |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-kat"></a>
### STOP_SYSTEMCHECK_KAT

0x32EB00 STOP_SYSTEMCHECK_KAT Ende Systemdiagnose KAT Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-diagnose-lsv"></a>
### STATUS_DIAGNOSE_LSV

0x31402C45 und 0x31402C46 STATUS_DIAGNOSE_LSV Status LSV-Diagnose auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZLSV_WERT | int | Status Zyklus-Flag LSV Bank 1 lesen |
| STAT_ZLSV2_WERT | int | Status Zyklus-Flag LSV Bank 2 lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_LSV_FLAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_LSV_FLAG | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_LSV2_FLAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_LSV2_FLAG | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lsh"></a>
### START_SYSTEMCHECK_LSH

0x31ED00 START_SYSTEMCHECK_LSH Start der Systemdiagnose LSH Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BANK | int | selektiert die Bank aus (1--&gt; Bank 1, 2--&gt; Bank 2, 3--&gt; Bank 1 und 2) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lsh"></a>
### STATUS_SYSTEMCHECK_LSH

0x31402C71 und 0x31402C72 STATUS_SYSTEMCHECK_LSH Status LSH-Diagnose auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZLSH_EIN | int | Status Zyklus-Flag LSH Bank 1 lesen |
| STAT_ZLSH2_EIN | int | Status Zyklus-Flag LSH Bank 2 lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_LSH_FLAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_LSH_FLAG | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_LSH2_FLAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_LSH2_FLAG | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lsh"></a>
### STOP_SYSTEMCHECK_LSH

0x32ED00 STOP_SYSTEMCHECK_LSH Ende der Systemdiagnose LSH Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-grundadapt"></a>
### START_SYSTEMCHECK_GRUNDADAPT

0x313200 START_SYSTEMCHECK_GRUNDADAPT Systemdiagnose Grundadaptionenen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-grundadapt"></a>
### STATUS_SYSTEMCHECK_GRUNDADAPT

0x2127 STATUS_SYSTEMCHECK_GRUNDADAPT Status Systemdiagnose Grundadaptionen starten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GAD_EIN | int | Status Grundadaption ein (B_gad) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-grundadapt"></a>
### STOP_SYSTEMCHECK_GRUNDADAPT

0x323200 STOP_SYSTEMCHECK_GRUNDADAPT Ende Systemdiagnose Grundadaptionen starten Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-gemischadapt-sperr"></a>
### START_SYSTEMCHECK_GEMISCHADAPT_SPERR

0x31D800 START_SYSTEMCHECK_GEMISCHADAPT_SPERR Systemdiagnose Gemischadaptionen sperren Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-gemischadapt-sperr"></a>
### STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR

0x32D800 STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR Ende Systemdiagnose Gemischadaptionen sperren Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lambda-aus"></a>
### START_SYSTEMCHECK_LAMBDA_AUS

0x31D900 START_SYSTEMCHECK_LAMBDA_AUS Systemdiagnose Labdaregelung aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lambda-aus"></a>
### STATUS_SYSTEMCHECK_LAMBDA_AUS

0x2118 STATUS_SYSTEMCHECK_LAMBDA_AUS Status Systemdiagnose Lambdaregelung aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAMBREGBANK1_TEXT | string | Status der Lambdaregelung Bank 1 (flglrs) |
| STAT_LAMBREGBANK2_TEXT | string | Status der Lambdaregelung Bank 2 (flglrs2) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lambda-aus"></a>
### STOP_SYSTEMCHECK_LAMBDA_AUS

0x32D900 STOP_SYSTEMCHECK_LAMBDA_AUS Ende Systemdiagnose Lambdaregelung aus Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-kompression"></a>
### START_SYSTEMCHECK_KOMPRESSION

0x31F300 START_SYSTEMCHECK_KOMPRESSION Systemdiagnose Kompressionstest Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-kompression"></a>
### STOP_SYSTEMCHECK_KOMPRESSION

0x32F300 STOP_SYSTEMCHECK_KOMPRESSION Ende Systemdiagnose Kompressiostest Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ruhestrommessung"></a>
### STEUERN_RUHESTROMMESSUNG

0x312B STEUERN_RUHESTROMMESSUNG Ansteuern Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_MAX_WERT | real | Max. Ruhestromschwelle (Eco_max_i) Eco_max_i   Einheit: A   Min: 0 Max: 0.3187 |
| MSB_WERT | real | Ecos Messtartbedingung (Eco_msb) Eco_msb   Einheit: s   Min: 0 Max: 12.75 |
| MZ_WERT | real | Dauer Mittelwertmessung (Eco_mz) Eco_mz   Einheit: s   Min: 0 Max: 12.75 |
| TO_WERT | unsigned long | Ecos Messung Timeout (Eco_timo) Eco_timo   Einheit: s   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ruhestrommessung"></a>
### STATUS_RUHESTROMMESSUNG

0x332B STATUS_RUHESTROMMESSUNG Auslesen Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RUHESTROM_TEXT | string | Funktionsstatus RUHESTROM (Eco_jobstat1) 1BYTE FUNKTIONSSTATUS |
| STAT_FS_RUHESTROM_WERT | int |  |
| STAT_STAT_RUHESTROM_WERT | real | Ruhestrom (Eco_result1) Eco_result1   Einheit: A   Min: 0 Max: 81.9187 |
| STAT_STAT_RUHESTROM_EINH | string | A |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-glf"></a>
### START_SYSTEMCHECK_GLF

0x31D5 START_SYSTEMCHECK_GLF Start Systemcheck 'geführte Luftsteuerung' Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-glf"></a>
### STOP_SYSTEMCHECK_GLF

0x32D5 STOP_SYSTEMCHECK_GLF Systemcheck 'geführte Luftsteuerung' beenden Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-glf"></a>
### STATUS_SYSTEMCHECK_GLF

0x33D5 STATUS_SYSTEMCHECK_GLF Stati Systemcheck 'geführte Luftsteuerung' Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_SYSTEMCHECK_GLF_WERT | int | Wert Statusbyte 1 |
| STAT_SYSTEMCHECK_GLF_TEXT | string | Text Statusbyte 1 |
| STAT_GLF_15_WERT | int | Wert High-Byte Statusword (Bit 7) |
| STAT_GLF_15_TEXT | string | Text High-Byte Statusword (Bit 7) |
| STAT_GLF_14_WERT | int | Wert High-Byte Statusword (Bit 6) |
| STAT_GLF_14_TEXT | string | Text High-Byte Statusword (Bit 6) |
| STAT_GLF_13_WERT | int | Wert High-Byte Statusword (Bit 5) |
| STAT_GLF_13_TEXT | string | Text High-Byte Statusword (Bit 5) |
| STAT_GLF_12_WERT | int | Wert High-Byte Statusword (Bit 4) |
| STAT_GLF_12_TEXT | string | Text High-Byte Statusword (Bit 4) |
| STAT_GLF_11_WERT | int | Wert High-Byte Statusword (Bit 3) |
| STAT_GLF_11_TEXT | string | Text High-Byte Statusword (Bit 3) |
| STAT_GLF_10_WERT | int | Wert High-Byte Statusword (Bit 2) |
| STAT_GLF_10_TEXT | string | Text High-Byte Statusword (Bit 2) |
| STAT_GLF_9_WERT | int | Wert High-Byte Statusword (Bit 1) |
| STAT_GLF_9_TEXT | string | Text High-Byte Statusword (Bit 1) |
| STAT_GLF_8_WERT | int | Wert High-Byte Statusword (Bit 0) |
| STAT_GLF_8_TEXT | string | Text High-Byte Statusword (Bit 0) |
| STAT_GLF_7_WERT | int | Wert Low-Byte Statusword (Bit 7) |
| STAT_GLF_7_TEXT | string | Text Low-Byte Statusword (Bit 7) |
| STAT_GLF_6_WERT | int | Wert Low-Byte Statusword (Bit 6) |
| STAT_GLF_6_TEXT | string | Text Low-Byte Statusword (Bit 6) |
| STAT_GLF_5_WERT | int | Wert Low-Byte Statusword (Bit 5) |
| STAT_GLF_5_TEXT | string | Text Low-Byte Statusword (Bit 5) |
| STAT_GLF_4_WERT | int | Wert Low-Byte Statusword (Bit 4) |
| STAT_GLF_4_TEXT | string | Text Low-Byte Statusword (Bit 4) |
| STAT_GLF_3_WERT | int | Wert Low-Byte Statusword (Bit 3) |
| STAT_GLF_3_TEXT | string | Text Low-Byte Statusword (Bit 3) |
| STAT_GLF_2_WERT | int | Wert Low-Byte Statusword (Bit 2) |
| STAT_GLF_2_TEXT | string | Text Low-Byte Statusword (Bit 2) |
| STAT_GLF_1_WERT | int | Wert Low-Byte Statusword (Bit 1) |
| STAT_GLF_1_TEXT | string | Text Low-Byte Statusword (Bit 1) |
| STAT_GLF_0_WERT | int | Wert Low-Byte Statusword (Bit 0) |
| STAT_GLF_0_TEXT | string | Text Low-Byte Statusword (Bit 0) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-glf"></a>
### STEUERN_GLF

0x30ED07FF000A STEUERN_GLF Stellgliedansteuerung GLF (obere Klappe) Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF_WERT | int | Klappe auf = 1, Klappe zu = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf"></a>
### STEUERN_ENDE_GLF

0x30ED00 STEUERN_ENDE_GLF Ansteuerung GLF (obere Klappe) beenden Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-glf"></a>
### STATUS_GLF

0x30ED01 STATUS_GLF Status obere und untere Klappe Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_STAT_GLF_WERT | int | "OKAY", wenn fehlerfrei |
| STAT_STAT_GLF_TEXT | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-glf2"></a>
### STEUERN_GLF2

0x30BE07FF000A STEUERN_GLF2 Stellgliedansteuerung GLF2 (untere Klappe) Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF2_WERT | int | Klappe auf = 1, Klappe zu = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf2"></a>
### STEUERN_ENDE_GLF2

0x30BE00 STEUERN_ENDE_GLF2 Stellgliedansteuerung GLF beenden Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-glf2"></a>
### STATUS_GLF2

0x30BE01 STATUS_GLF2 Status obere und untere Klappe Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_STAT_GLF2_WERT | int | "OKAY", wenn fehlerfrei |
| STAT_STAT_GLF2_TEXT | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa-anschlag"></a>
### STEUERN_DISA_ANSCHLAG

0x31E600 STEUERN_DISA_ANSCHLAG lernen der DISA-Anschlaege Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-disa-anschlag"></a>
### STATUS_DISA_ANSCHLAG

0x212A STATUS_DISA_ANSCHLAG Status Lernen der DISA-Anschlaege Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISA_ANSCHL | int | Status des Lernens Disa |
| STAT_DISA_ANSCHL_TEXT | string | Status des Lernens Disa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-disa-anschlag"></a>
### STOP_DISA_ANSCHLAG

0x32E600 STOP_DISA_ANSCHLAG Ende des Lernes DISA-Anschlaege Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-minhub"></a>
### STATUS_MINHUB

0x30A301 STATUS_MINHUB Auslesen VVT-Minhub Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MINHUB_WERT | real | Wert von minhub_w |
| STAT_MINHUB_EINH | string | Einheit von minhub_w |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-minhub"></a>
### STEUERN_MINHUB

0x22400F STEUERN_MINHUB VVT-Minhub vorgeben Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MINHUB | int | Vorsteuerwert minhubvs_w in tausendstel Milimeter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-minhub-programm"></a>
### STEUERN_MINHUB_PROGRAMM

0x30A308010000 STEUERN_MINHUB_PROGRAMM Programmieren VVT-Minhub Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MINHUB | int | zu programmierender Wert minhubvs_w in tausendstel Milimeter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bankabgleich"></a>
### STATUS_BANKABGLEICH

0x30A401 STATUS_BANKABGLEICH Auslesen des VVT-Bankabgleiches Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFWTSTBER_WERT | real | Wert von ofwtstber (=Dummy) |
| STAT_OFWTSTBER_EINH | string | Einheit von ofwtstber (=Dummy) |
| STAT_OFWNKTEST_WERT | real | Wert von ofwnktest (= Offset Verstellwinkel Excenterwelle) |
| STAT_OFWNKTEST_EINH | string | Einheit von ofwnktest [Grad] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bankabgleich-programm"></a>
### STEUERN_BANKABGLEICH_PROGRAMM

0x30A408010000 STEUERN_BANKABGLEICH_PROGRAMM Programmieren des Winkeloffset Excenterwelle (ofwnktest) Verstellbereich Bank 1: 0°...5° Verstellbereich Bank 2: 0°...-5° Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OFWTSTBER | int | Offsetbereich, nur ein Dummy, wird nicht ausgewertet |
| OFWNKTEST | int | Eingabewert für Winkeloffset (Eingabebereich: -50....50) zB: OFWNKTEST = 30  =&gt; ofwnktest = 3° |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

0x21C3 STATUS_BETRIEBSSTUNDENZAEHLER Status Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZ | string | Status Betriebsstundenzaehler lesen |
| STAT_BSZ_WERT | int | Status Betriebsstundenzaehler (int) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dme-startwert-abgleich"></a>
### DME_STARTWERT_ABGLEICH

Kopiert die ISN auf beide Wechselcodes KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $20 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ews-startwert"></a>
### EWS_STARTWERT

0x318300 EWS_STARTWERT EWS-Startwertinitialisierung Aktivierung: Klemme 15 = EIN Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | int | Parameter zur Initialisierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EWS_STATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| STAT_EWS_WERT | int | Rueckgabewert bei der Startwertinitialisierung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ews-empfang"></a>
### EWS_EMPFANG

0x2106 EWS_EMPFANG EWS-Empfangsstatus auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EWS_EMPFANGSSTATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| EWS_STATUS_VALUE | int | Rueckgabestatus bei der Startwertinitialisierung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

0x224000 STATUS_MOTORTEMPERATUR Auslesen der Motortemperatur Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MOTORTEMPERATUR_WERT | real | Wert von tmot |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit von tmot |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

0x224000 STATUS_MOTORDREHZAHL Auslesen der Motordrehzahl Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORDREHZAHL_WERT | real | Wert von Motordrehzahl |
| STAT_MOTORDREHZAHL_EINH | string | Einheit von Motordrehzahl |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

0x224000 STATUS_AN_LUFTTEMPERATUR Auslesen der Lufttemperatur Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Wert von Lufttemperatur |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit von Lufttemperatur |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

0x224000 STATUS_LMM_MASSE Auslesen der Luftmasse Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_LMM_MASSE_WERT | real | Wert von Luftmasse |
| STAT_LMM_MASSE_EINH | string | Einheit von Luftmasse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

0x224003 STATUS_L_SONDE Auslesen der Lambdasondenspannung vorne Bank 1 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_WERT | real | Wert der Lambdasonden Spg. |
| STAT_L_SONDE_EINH | string | Einheit der Lambdasonden Spg. |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

0x224003 STATUS_L_SONDE_2 Auslesen der Lambdasondenspannung vorne Bank 2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_2_WERT | real | Wert der Lambdasonden Spg. |
| STAT_L_SONDE_2_EINH | string | Einheit der Lambdasonden Spg. |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-h"></a>
### STATUS_L_SONDE_H

0x304801 STATUS_L_SONDE_H Auslesen der Lambdasondenspannung hinten Bank 1 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_H_WERT | real | Wert der hinteren Lambdasonden Spg. |
| STAT_L_SONDE_H_EINH | string | Einheit der hinteren Lambdasonden Spg. |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2-h"></a>
### STATUS_L_SONDE_2_H

0x304501 STATUS_L_SONDE_2_H Auslesen der Lambdasondenspannung hinten Bank 2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_2_H_WERT | real | Wert der hinteren Lambdasonden Spg. Bank 2 |
| STAT_L_SONDE_2_H_EINH | string | Einheit der hinteren Lambdasonden Spg. Bank 2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-int"></a>
### STATUS_INT

0x224000 STATUS_INT Auslesen der Lambdaregelung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_INT_WERT | real | Wert der Lambdasondenregelung |
| STAT_INT_EINH | string | Einheit der Lambdasondenregelung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-int-2"></a>
### STATUS_INT_2

0x224000 STATUS_INT_2 Auslesen der Lambdaregelung Bank 2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_INT_2_WERT | real | Wert der Lambdasondenregelung Bank 2 |
| STAT_INT_2_EINH | string | Einheit der Lambdasondenregelung Bank 2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add"></a>
### STATUS_ADD

0x224004 STATUS_ADD Auslesen der additiven Lambdaregelung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ADD_WERT | real | Wert des additiven Lambdaregelung |
| STAT_ADD_EINH | string | Einheit des additiven Lambdaregelung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add-2"></a>
### STATUS_ADD_2

0x224004 STATUS_ADD_2 Auslesen der additiven Lambdaregelung Bank 2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ADD_2_WERT | real | Wert des additiven Lambdaregelung Bank 2 |
| STAT_ADD_2_EINH | string | Einheit des additiven Lambdaregelung Bank 2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mul"></a>
### STATUS_MUL

0x224004 STATUS_MUL Auslesen der multipikativen Lambdaregelung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MUL_WERT | real | Wert des multiplikativen Lambdaregelung |
| STAT_MUL_EINH | string | Einheit des multiplikativen Lambdaregelung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mul-2"></a>
### STATUS_MUL_2

0x224004 STATUS_MUL_2 Auslesen der multipikativen Lambdaregelung Bank 2 Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MUL_2_WERT | real | Wert des multiplikativen Lambdaregelung Bank 2 |
| STAT_MUL_2_EINH | string | Einheit des multiplikativen Lambdaregelung Bank 2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motorlaufunruhe"></a>
### STATUS_MOTORLAUFUNRUHE

0x224003 STATUS_MOTORLAUFUNRUHE Auslesen der Laufunruhewerte Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ZYL1_WERT | real | Wert von LUTSFI1 |
| STAT_ZYL2_WERT | real | Wert von LUTSFI2 |
| STAT_ZYL3_WERT | real | Wert von LUTSFI3 |
| STAT_ZYL4_WERT | real | Wert von LUTSFI4 |
| STAT_ZYL5_WERT | real | Wert von LUTSFI5 |
| STAT_ZYL6_WERT | real | Wert von LUTSFI6 |
| STAT_ZYL7_WERT | real | Wert von LUTSFI7 |
| STAT_ZYL8_WERT | real | Wert von LUTSFI8 |
| STAT_LAUFUNRUHE_EINH | string | Einheit in (1/min/s)^2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

0x224000 STATUS_UBATT Auslesen der Batteriespannung Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_UBATT_WERT | real | Wert der Batterie-Spg. |
| STAT_UBATT_EINH | string | Einheit der Batterie-Spg. |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geberrad-adaption"></a>
### STATUS_GEBERRAD_ADAPTION

0x224006 STATUS_GEBERRAD_ADAPTION Auslesen der NWG-Adaptionen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_GEBERRAD_ADAPTION_VSA_WERT | real | Wert von vsa_adp |
| STAT_GEBERRAD_ADAPTION_VSA_EINH | string | Wert von vsa_adp Einheit in Grd KW |
| STAT_GEBERRAD_ADAPTION_VSA_2_WERT | real | Wert von vsa2_adp |
| STAT_GEBERRAD_ADAPTION_VSA_2_EINH | string | Wert von vsa2_adp Einheit in Grd KW |
| STAT_GEBERRAD_ADAPTION_VSE_WERT | real | Wert von vse_adp |
| STAT_GEBERRAD_ADAPTION_VSE_EINH | string | Wert von vse_adp Einheit in Grd KW |
| STAT_GEBERRAD_ADAPTION_VSE_2_WERT | real | Wert von vse2_adp |
| STAT_GEBERRAD_ADAPTION_VSE_2_EINH | string | Wert von vse2_adp Einheit in Grd KW |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

0x224002 & 0x224007 STATUS_DIGITAL Auslesen der Schalter- und Funktionsstati Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KL15_EIN | int | Bedingung KL15 ein |
| STAT_ESTART_EIN | int | Bedingung Startrelais |
| STAT_KUP_EIN | int | Bedingung Kupplung betaetigt |
| STAT_BLS_EIN | int | Bedingung Bremsschalter ein |
| STAT_BLTS_EIN | int | Bedingung Bremslichttestschalter ein |
| STAT_KO_EIN | int | Bedingung Klimakompressor ein |
| STAT_AC_EIN | int | Dummy fuer Klimaanforderung (entspricht Klimakompressor ein) |
| STAT_LL_EIN | int | Zustand Leerlauf erreicht |
| STAT_VL_EIN | int | Zustand Vollast erreicht |
| STAT_SBBHK2_EIN | int | Lambdasondenbereitschaft hinter Kat Bank 2 |
| STAT_SBBHK_EIN | int | Lambdasondenbereitschaft hinter Kat Bank 1 |
| STAT_SBBVK2_EIN | int | Lambdasondenbereitschaft vor Kat Bank 2 |
| STAT_SBBVK_EIN | int | Lambdasondenbereitschaft vor Kat Bank 1 |
| STAT_LR2_EIN | int | Zustand Lambdaregelung Bank 2 ein |
| STAT_LR_EIN | int | Zustand Lambdaregelung Bank 1 ein |
| STAT_KD_EIN | int | Zustand KickDown ein |
| STAT_PN_EIN | int | Zustand Park-Neutral ein |
| STAT_ECULOCK_EIN | int | Zustand EWS_OK ein |
| STAT_TEHB_EIN | int | Zustand TEHB ein |
| STAT_SA_EIN | int | Zustand Schubabschneiden ein |
| STAT_LRNRDY_EIN | int | Zustand UMA Lernerfolg |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

0x304601 & 0x304701 STATUS_PWG_POTI_SPANNUNG Auslesen des Pedalwertgebers Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Wert von upwg1_w |
| STAT_PWG_POTI_SPANNUNG_2_WERT | real | Wert von upwg2_w |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit in V |
| _TEL_AUFTRAG_POTI1 | binary | Hex-Auftrag an SG für Poti-Spannung 1 |
| _TEL_ANTWORT_POTI1 | binary | Hex-Antwort von SG für Poti-Spannung 1 |
| _TEL_AUFTRAG_POTI2 | binary | Hex-Auftrag an SG für Poti-Spannung 2 |
| _TEL_ANTWORT_POTI2 | binary | Hex-Antwort von SG für Poti-Spannung 2 |

<a id="job-status-messwerte-ibs"></a>
### STATUS_MESSWERTE_IBS

0x22402B STATUS_MESSWERTE_IBS Auslesen von Temperatur, Spannung und Strom der Batterie Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TBATT_IBS_WERT | real | Wert von tbatt |
| STAT_TBATT_IBS_EINH | string | Einheit von tbatt |
| STAT_UBATT_IBS_WERT | real | Wert von ubatt_w |
| STAT_UBATT_IBS_EINH | string | Einheit von ubatt_w |
| STAT_IBATT_IBS_WERT | real | Wert von ibatt_w |
| STAT_IBATT_IBS_EINH | string | Einheit von ibatt_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-gen"></a>
### STATUS_MESSWERTE_GEN

0x22402C STATUS_MESSWERTE_GEN Auslesen der Generator-Messwerte Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_GENMANUFAK_WERT | string | Wert von genmanufak (Herstellercode Generator 1) |
| STAT_GENTYPKENN_WERT | string | Wert von gentypkenn (Kennung Generatortyp Generator 1) |
| STAT_BSDGENREGV_WERT | string | Wert von bsdgenregv (Reglerversion Generator 1) |
| STAT_DFFGEN_WERT | real | Wert von dffgen (Auslastungsgrad Generator 1) |
| STAT_DFFGEN_EINH | string | Einheit von dffgen (Auslastungsgrad Generator 1) |
| STAT_UGEN_WERT | real | Wert von ugen (Generatorsollspannung) |
| STAT_UGEN_EINH | string | Einheit von ugen (Generatorsollspannung) |
| STAT_UFGEN_WERT | real | Wert von ufgen (Kopie Generatorsollspannung) |
| STAT_UFGEN_EINH | string | Einheit ufgen (Kopie Generatorsollspannung) |
| STAT_TLRGEN_WERT | real | Wert von tlrgen (Eingangswert Loadresponse Zeit) |
| STAT_TLRGEN_EINH | string | Einheit von tlrgen (Eingangswert Loadresponse Zeit) |
| STAT_TLRFGEN_WERT | real | Wert von tlrfgen (Kopie Eingangswert Loadresponse Zeit) |
| STAT_TLRFGEN_EINH | string | Einheit von tlrfgen (Kopie Eingangswert Loadresponse Zeit) |
| STAT_MDGENVF_WERT | real | Wert von mdgenvf_w (gefiltertes Generatormoment) |
| STAT_MDGENVF_EINH | string | Einheit von mdgenvf_w (gefiltertes Generatormoment) |
| STAT_BLRFOFF_WERT | int | Wert von B_lrfoff (Drehzahlschwelle für Loadresponse-Funktion Gen.1 aktiv) |
| STAT_STIGEN_WERT | real | Wert von st_i_gen (Generatorstrom) |
| STAT_STIGEN_EINH | string | Einheit von st_i_gen (Generatorstrom) |
| STAT_IERR_WERT | real | Wert von ierr (Erregerstrom Generator 1) |
| STAT_IERR_EINH | string | Einheit von ierr (Erregerstrom Generator 1) |
| STAT_IERRGRENZ_WERT | real | Wert von ierrgrenz (begrenzter Erregerstrom Generator 1) |
| STAT_IERRGRENZ_EINH | string | Einheit von ierrgrenz (begrenzter Erregerstrom Generator 1) |
| STAT_IERRFGRENZ_WERT | real | Wert von ierrfgrenz (Kopie begrenzter Erregerstrom Generator 1) |
| STAT_IERRFGRENZ_EINH | string | Einheit von ierrfgrenz (Kopie begrenzter Erregerstrom Generator 1) |
| STAT_TCHIP_WERT | real | Wert von tchip (Chiptemperatur Generator 1) |
| STAT_TCHIP_EINH | string | Einheit von tchip (Chiptemperatur Generator 1) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-vad"></a>
### STATUS_MESSWERTE_VAD

0x224025 STATUS_MESSWERTE_VAD Variantenadaptionen auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FHA_VAD_WERT | real | Hinterachsuebersetzung (Wert von fakiha) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ibs"></a>
### IDENT_IBS

0x224021 IDENT_IBS Identifikationsdaten für IBS auslesen (BMW Nr, Seriennummer, SW/HW Index) Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ID_BMW_NR | string | BMW-Teilenummer 7 stellig |
| SERIENNUMMER | unsigned long | BMW-Seriennummer |
| ZIF_PROGRAMMSTAND | int | Programm referenz |
| ZIF_STATUS | int | Programm Revision |
| HW_REF | int | Hardware Referenz |

<a id="job-status-systemcheck-pm-info-1"></a>
### STATUS_SYSTEMCHECK_PM_INFO_1

0x224022 STATUS_SYSTEMCHECK_PM_INFO_1 Batterie Powermanagement Bytefeld 1 lesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_RUHESTROMANALYSE_MODE_WERT | int | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_RUHESTROMANALYSE_MODE_TEXT | string | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_BATTERIELADUNG_BILANZ_WERT | real | Differenz LADUNG - ENTLADUNG in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Einheit |
| STAT_BATTERIELADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Einheit |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_EINH | string | Einheit |
| STAT_KM_STAND_AKTUELL_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_AKTUELL_EINH | string | Einheit |
| STAT_KM_STAND_VOR_1_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_2_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_3_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_4_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_5_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_LETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_DRITTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_DRITTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_VIERTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_VIERTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_EINH | string | Einheit |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | real | 0 - 19088 Ah |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | Einheit Ah |
| STAT_RUHESTROM_AKTUELL | string |  |
| STAT_RUHESTROM_VOR_1_ZYKLUS | string |  |
| STAT_RUHESTROM_VOR_2_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_3_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_4_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_5_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_6_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_7_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_8_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_9_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_10_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_11_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_12_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_13_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_14_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_15_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_16_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_17_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_18_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_19_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_20_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_21_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_22_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_23_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_24_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_25_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_26_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_27_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_28_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_29_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_30_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_31_ZYKLEN | string |  |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_EINH | string | Einheit |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_WERT | real | Anzahl 0 - 65535 |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_BSD_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_BSD_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_EINH | string | Einheit |

<a id="job-status-systemcheck-pm-info-2"></a>
### STATUS_SYSTEMCHECK_PM_INFO_2

0x224023 STATUS_SYSTEMCHECK_PM_INFO_2 Batterie Powermanagement Bytefeld 2 lesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BATTERIE_KAPAZITAET_WERT | real | Batterie Kapazitaet in Ah 0 - 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Einheit |
| STAT_SOH_WERT | real | Bereich -50% - 49,6% |
| STAT_SOH_EINH | string | Einheit |
| STAT_SOC_FIT_WERT | real | Bereich 0-100% |
| STAT_SOC_FIT_EINH | string | Einheit |
| STAT_TEMP_SAISON_WERT | real | Bereich -128C - 127C |
| STAT_TEMP_SAISON_EINH | string | Einheit C |
| STAT_KALIBRIER_EVENT_CNT_WERT | real | Kalibrieranzahl 0 - 255 |
| STAT_KALIBRIER_EVENT_CNT_EINH | string | Einheit |
| STAT_Q_SOC_AKTUELL_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Einheit |
| STAT_Q_SOC_VOR_1_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_2_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_3_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_4_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_5_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_EINH | string | Einheit |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

0x2E5FF504 STEUERN_PM_HISTOGRAM_RESET Löschen der Powermanagement-Infofelder Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adap-selektiv-loeschen"></a>
### ADAP_SELEKTIV_LOESCHEN

0x3130 ADAP_SELEKTIV_LOESCHEN Löschen von Adaptionen und gelernte Varianten Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_2 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_3 | int | Bit=1 löscht Bit=0 behält alten Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

0x3130001000 STEUERN_BATTERIETAUSCH_REGISTRIEREN Batterietausch registrieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-pm-messemode"></a>
### START_SYSTEMCHECK_PM_MESSEMODE

0x31F6 START_SYSTEMCHECK_PM_MESSEMODE Systemdiagnose BatterieSensor Messemode setzen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-pm-messemode"></a>
### STOP_SYSTEMCHECK_PM_MESSEMODE

0x32F6 STOP_SYSTEMCHECK_PM_MESSEMODE Systemdiagnose BatterieSensor Messmode beenden Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-igrinfo"></a>
### _STATUS_IGRINFO

0x224016 _STATUS_IGRINFO Infospeicher Intelligente Generator Regelung (IGR) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IGR1_BITS7 | unsigned long | Begrenzung 2 1BIT IDENTICAL |
| STAT_IGR1_BITS6 | unsigned long | Begrenzung 1 1BIT IDENTICAL |
| STAT_IGR1_BITS5 | unsigned long | Regeneration 1BIT IDENTICAL |
| STAT_IGR1_BITS4 | unsigned long | IGR-Medium 1BIT IDENTICAL |
| STAT_IGR1_BITS3 | unsigned long | IGR-High 1BIT IDENTICAL |
| STAT_IGR1_BITS2 | unsigned long | IGR-Low 1BIT IDENTICAL |
| STAT_IGR1_BITS1 | unsigned long | Diagnosejob gesetzt 1BIT IDENTICAL |
| STAT_IGR1_BITS0 | unsigned long | IGR codiert 1BIT IDENTICAL |
| STAT_IGR2_BITS7 | unsigned long | Zyklisierung MSA 1BIT IDENTICAL |
| STAT_IGR2_BITS6 | unsigned long | Begrenzung DS 1BIT IDENTICAL |
| STAT_IGR2_BITS5 | unsigned long | Begrenzung TS 1BIT IDENTICAL |
| STAT_IGR2_BITS4 | unsigned long | Begrenzung TB 1BIT IDENTICAL |
| STAT_IGR2_BITS3 | unsigned long | Begrenzung M 1BIT IDENTICAL |
| STAT_IGR2_BITS2 | unsigned long | Begrenzung G 1BIT IDENTICAL |
| STAT_IGR2_BITS1 | unsigned long | Begrenzung W 1BIT IDENTICAL |
| STAT_IGR2_BITS0 | unsigned long | Begrenzung L 1BIT IDENTICAL |
| STAT_IGR3_BITS7 | unsigned long | IGR Res2 1BIT IDENTICAL |
| STAT_IGR3_BITS6 | unsigned long | IGR Res1 1BIT IDENTICAL |
| STAT_IGR3_BITS5 | unsigned long | IGR-Hi Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS4 | unsigned long | IGR-Med Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS3 | unsigned long | IGR-Low Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS2 | unsigned long | IGR-Hi Enabled 1BIT IDENTICAL |
| STAT_IGR3_BITS1 | unsigned long | IGR-Med Enabled 1BIT IDENTICAL |
| STAT_IGR3_BITS0 | unsigned long | IGR-Low Enabled 1BIT IDENTICAL |
| STAT_IGR_PR1 | unsigned long | Level BN Soll 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_PR2 | unsigned long | Level Soll 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_ANTL_WERT | real | Anteil Low 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTL_EINH | string | percent |
| STAT_IGR_ANTM_WERT | real | Anteil Medium 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTM_EINH | string | percent |
| STAT_IGR_ANTH_WERT | real | Anteil High 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTH_EINH | string | percent |
| STAT_IGR_11 | unsigned long | Anteil 11 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_12 | unsigned long | Anteil 12 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_M_AGO_WERT | unsigned long | Abstand zu letzter Mediumphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_M_AGO_EINH | string | Minute |
| STAT_IGR_H_AGO_WERT | unsigned long | Abstand zu letzter Highphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_H_AGO_EINH | string | Minute |
| STAT_IGR_BSA1 | unsigned long | Zaehler Low 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_IGR_QLAD_WERT | real | Bilanz Low 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_QLAD_EINH | string | Ah |
| STAT_IGR_QLAD_M_WERT | long | Bilanz Medium 1BYTE in -128 bis +127 Ah   Einheit: Ah   Min: -128 Max: 127 |
| STAT_IGR_QLAD_M_EINH | string | Ah |
| STAT_IGR_QELAD_WERT | real | Bilanz High 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_QELAD_EINH | string | Ah |
| STAT_IGR_TMED_WERT | unsigned long | Dauer letzte Mediumphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_TMED_EINH | string | Minute |
| STAT_IGR_THIGH_WERT | unsigned long | Dauer letzte Highphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_THIGH_EINH | string | Minute |
| STAT_IGR_TCODE | unsigned long | Dauer iGR-Codiert 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_IGR_HIGH | unsigned long | Zaehler High 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_ZR | unsigned long | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_SEIT_WERT | unsigned long | Zeit seit letzter R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_SEIT_EINH | string | h |
| STAT_REG_DAUER_WERT | unsigned long | Dauer letzte R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_DAUER_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-leminfo"></a>
### _STATUS_LEMINFO

0x224017 _STATUS_LEMINFO Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen Aktivierung: Klemme 15 = EIN Activation:

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZR_USTAT_A | unsigned long | Haeufigkeitszaehler Zr_ustat_A 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_B | unsigned long | Haeufigkeitszaehler Zr_ustat_B 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_C | unsigned long | Haeufigkeitszaehler Zr_ustat_C 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_D | unsigned long | Haeufigkeitszaehler Zr_ustat_D 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_E | unsigned long | Haeufigkeitszaehler Zr_ustat_E 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_F | unsigned long | Haeufigkeitszaehler Zr_ustat_F 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_G | unsigned long | Haeufigkeitszaehler Zr_ustat_G 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_UBSTUFE_L | unsigned long | Haeufigkeitszaehler Zr_ubstufe_L 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UBSTUFE_H | unsigned long | Haeufigkeitszaehler Zr_ubstufe_H 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_A | unsigned long | Haeufigkeitszaehler Zr_uquali_A 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_B | unsigned long | Haeufigkeitszaehler Zr_uquali_B 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_C | unsigned long | Haeufigkeitszaehler Zr_uquali_C 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_IERRLLRED | unsigned long | Haeufigkeitszaehler Zr_ierrllred 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_TM_IERRLLRED_WERT | unsigned long | Mittelwert Tm_ierrllred 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_IERRLLRED_EINH | string | second |
| STAT_ZR_IERRTRED | unsigned long | Haeufigkeitszaehler Zr_ierrtred 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_TM_IERRTRED_WERT | unsigned long | Mittelwert Tm_ierrtred 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |
| STAT_TM_IERRTRED_EINH | string | second |
| STAT_TM_ENTLFUNK_WERT | unsigned long | Mittelwert Tm_entlfunk 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_ENTLFUNK_EINH | string | second |
| STAT_ZR_ENTLFUNK | unsigned long | Haeufigkeitszaehler Zr_entlfunk 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_ENTLFUNKVOLL | unsigned long | Haeufigkeitszaehler Zr_entlfunkvoll 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_ENTLFUNKNIX | unsigned long | Haeufigkeitszaehler Zr_entlfunknix 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_ENTLFUNKTEIL | unsigned long | Haeufigkeitszaehler Zr_entlfunkteil 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_TM_ENTLSICH_WERT | unsigned long | Mittelwert Tm_entlsich 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_ENTLSICH_EINH | string | second |
| STAT_ZR_ENTLSICH | unsigned long | Haeufigkeitszaehler Zr_entelsich 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| STAT_ZR_ENTLSICHVOLL | unsigned long | Haeufigkeitszaehler Zr_entelsichvoll 2BYTE in 0 bis 65535   Min: 0 Max: 65535 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (12 × 2)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [CBSKENNUNG](#table-cbskennung) (17 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (277 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (12 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (277 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (163 × 9)
- [FARTTYP](#table-farttyp) (275 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (320 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [BETRIEBSWTAB](#table-betriebswtab) (256 × 13)
- [BITS](#table-bits) (124 × 4)
- [VVTSTATUSBG2_2](#table-vvtstatusbg2-2) (8 × 2)
- [EWSSTART](#table-ewsstart) (5 × 2)
- [EWSEMPFANGSSTATUS](#table-ewsempfangsstatus) (15 × 2)
- [REGEL](#table-regel) (7 × 2)
- [TEVSTATUS](#table-tevstatus) (9 × 2)
- [STAGEDMTL](#table-stagedmtl) (19 × 2)
- [STAGEDMTLFREEZE](#table-stagedmtlfreeze) (23 × 2)
- [LSUSTATUS](#table-lsustatus) (3 × 2)
- [LSUSTATUS_NEU](#table-lsustatus-neu) (12 × 2)
- [DISASTATUS](#table-disastatus) (9 × 2)
- [LAMBDASTATUS](#table-lambdastatus) (6 × 2)
- [BETRIEBSSTUNDENSTATUS](#table-betriebsstundenstatus) (4 × 2)
- [KATSTATUS](#table-katstatus) (7 × 2)
- [_ME923_CNV_S_2_DEF_BIT_UB_741_CM](#table-me923-cnv-s-2-def-bit-ub-741-cm) (2 × 2)
- [_ME923_CNV_S_2_DEF_BIT_UB_755_CM](#table-me923-cnv-s-2-def-bit-ub-755-cm) (2 × 2)
- [_ME923_CNV_S_2_DEF_BIT_UB_755_CM0X2](#table-me923-cnv-s-2-def-bit-ub-755-cm0x2) (2 × 2)
- [_ME923_TABLE_ST_GENTEST](#table-me923-table-st-gentest) (8 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT0](#table-me923-table-geniutest-err-bit0) (2 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT1](#table-me923-table-geniutest-err-bit1) (2 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT2](#table-me923-table-geniutest-err-bit2) (2 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT3](#table-me923-table-geniutest-err-bit3) (2 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT4](#table-me923-table-geniutest-err-bit4) (2 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT5](#table-me923-table-geniutest-err-bit5) (2 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT6](#table-me923-table-geniutest-err-bit6) (2 × 2)
- [_ME923_TABLE_GENIUTEST_ERR_BIT7](#table-me923-table-geniutest-err-bit7) (2 × 2)
- [_ME923_TABLE_GENIUTEST_AB_BIT0](#table-me923-table-geniutest-ab-bit0) (2 × 2)
- [_ME923_TABLE_FS](#table-me923-table-fs) (10 × 2)
- [STAT_RUHESTROM](#table-stat-ruhestrom) (17 × 2)

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
| 0x20 | Fehler momentan nicht vorhanden, nicht OBD-entprellt |
| 0x21 | Fehler momentan nicht vorhanden, OBD-entprellt |
| 0x22 | Fehler momentan vorhanden, noch nicht OBD-entprellt |
| 0x23 | Fehler momentan vorhanden, OBD-entprellt |
| 0x30 | Fehler verursacht kein Aufleuchten der Warnlampe (MIL) |
| 0x31 | Fehler wuerde das Aufleuchten der Warnlampe (MIL) verursachen |
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

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 17 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | CSF | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x09 | VTG | Verteilergetriebeoel |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x13 | H2 | H2-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x16 | DAD | Additiv fuer Partikelfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x0A | ZKrz_a | Zuendkerzen adaptiv |

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
| 2 | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 277 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0000 | 0000 FehlerOrt nicht bedatet |
| 0x29CC | CDKMD - Verbrennungsaussetzer, mehrere Zylinder |
| 0x29CD | CDKMD00 - Verbrennungsaussetzer, Zylinder 1 |
| 0x29CE | CDKMD07 - Verbrennungsaussetzer, Zylinder 2 |
| 0x29CF | CDKMD05 - Verbrennungsaussetzer, Zylinder 3 |
| 0x29D0 | CDKMD02 - Verbrennungsaussetzer, Zylinder 4 |
| 0x29D1 | CDKMD01 - Verbrennungsaussetzer, Zylinder 5 |
| 0x29D2 | CDKMD04 - Verbrennungsaussetzer, Zylinder 6 |
| 0x29D3 | CDKMD06 - Verbrennungsaussetzer, Zylinder 7 |
| 0x29D4 | CDKMD03 - Verbrennungsaussetzer, Zylinder 8 |
| 0x29D9 | CDKCPFLL - Verbrennungsaussetzer bei geringem Tankfüllstand |
| 0x29DD | CDKSWE - Schlechtwegstreckenerkennung |
| 0x29E5 | CDKFRAO - Gemischadaption, oberer Drehzahlbereich |
| 0x29E6 | CDKFRAO2 - Gemischadaption 2, oberer Drehzahlbereich |
| 0x29E7 | CDKRKAT - Gemischadaption im Leerlauf pro Zeit |
| 0x29E8 | CDKRKAT2 - Gemischadaption 2 im Leerlauf pro Zeit |
| 0x29ED | CDKFRAU - Gemischadaption, unterer Drehzahlbereich |
| 0x29EE | CDKFRAU2 - Gemischadaption 2, unterer Drehzahlbereich |
| 0x29EF | CDKFMAS - Gemischadaption, Summenfehler |
| 0x29F0 | CDKFMAS2 - Gemischadaption 2, Summenfehler |
| 0x29F4 | CDKKAT - Katalysatorkonvertierung |
| 0x29F5 | CDKKAT2 - Katalysatorkonvertierung 2 |
| 0x29FA | CDKMDKH - Katalysatorheizung |
| 0x2A12 | CDKDMMVE - DMTL-Magnetventil, Ansteuerung |
| 0x2A13 | CDKDMPME - DMTL-Leckdiagnosepumpe, Ansteuerung |
| 0x2A14 | CDKDMTK - DMTL, Feinstleck |
| 0x2A15 | CDKTESG - DMTL, Feinleck |
| 0x2A16 | CDKDMTKNM - DMTL, Feinstleck |
| 0x2A17 | CDKDMTL - DMTL, Systemfehler |
| 0x2A18 | CDKDHDMTE - DMTL, Heizung: Ansteuerung |
| 0x2A19 | CDKTEVE - Tankentlüftungsventil, Ansteuerung |
| 0x2A1A | CDKTES - Tankentlüftungssystem, Funktion |
| 0x2A1D | CDKFSTP - Tankfüllstand, Plausibilität |
| 0x2A1E | CDKFSTSI - Tankfüllstand, Signal |
| 0x2A58 | CDKVVTE - Valvetronic,  Spannungsversorgung |
| 0x2A59 | CDKDVFFS - Valvetronic, Exzenterwellensensor: Führung |
| 0x2A5A | CDKDVFFS2 - Valvetronic, Exzenterwellensensor 2: Führung |
| 0x2A5B | CDKDVFRS - Valvetronic, Exzenterwellensensor: Referenz |
| 0x2A5C | CDKDVFRS2 - Valvetronic, Exzenterwellensensor 2: Referenz |
| 0x2A5D | CDKDVPLA - Valvetronic, Exzenterwellensensor: Plausibilität |
| 0x2A5E | CDKDVPLA2 - Valvetronic, Exzenterwellensensor 2: Plausibilität |
| 0x2A5F | CDKDVUSE - Valvetronic, Exzenterwellensensor: Spannungsversorgung |
| 0x2A60 | CDKDVUSE2 - Valvetronic, Exzenterwellensensor 2: Spannungsversorgung |
| 0x2A61 | CDKDVLRN - Valvetronic, Verstellbereich |
| 0x2A62 | CDKDVLRN2 - Valvetronic, Verstellbereich 2 |
| 0x2A63 | CDKDVSTE - Valvetronic, Stellmotor: Überwachung Schwergängigkeit, Drehrichtung |
| 0x2A64 | CDKDVSTE2 - Valvetronic, Stellmotor 2: Überwachung Schwergängigkeit, Drehrichtung |
| 0x2A65 | CDKDVFSG - Valvetronic,  interner Fehler |
| 0x2A66 | CDKDVFSG2 - Valvetronic,  interner Fehler 2 |
| 0x2A67 | CDKDVEST - Valvetronic, Stellmotor: Ansteuerung |
| 0x2A68 | CDKDVEST2 - Valvetronic, Stellmotor 2: Ansteuerung |
| 0x2A69 | CDKDVULV - Valvetronic, Stellmotor: Spannungsversorgung |
| 0x2A6A | CDKDVULV2 - Valvetronic, Stellmotor 2: Spannungsversorgung |
| 0x2A6B | CDKDVPMN - Valvetronic, Leistungsbegrenzung |
| 0x2A6C | CDKDVAN - Valvetronic, Position bei Neustart: Plausibilität |
| 0x2A6D | CDKDVOVL - Valvetronic, elektrischer Überlastschutz |
| 0x2A6E | CDKDVOVL2 - Valvetronic, elektrischer Überlastschutz 2 |
| 0x2A6F | CDKMINHUB - Valvetronic, Minimalhub |
| 0x2A80 | CDKENWSE - Einlass-VANOS, Ansteuerung |
| 0x2A81 | CDKENWSE2 - Einlass-VANOS, Ansteuerung 2 |
| 0x2A83 | CDKENWS - Einlass-VANOS |
| 0x2A84 | CDKENWS2 - Einlass-VANOS 2 |
| 0x2A85 | CDKANWSE - Auslass-VANOS, Ansteuerung |
| 0x2A86 | CDKANWSE2 - Auslass-VANOS, Ansteuerung 2 |
| 0x2A88 | CDKANWS - Auslass-VANOS |
| 0x2A89 | CDKANWS2 - Auslass-VANOS 2 |
| 0x2A8A | CDKENWSAD - Einlass-VANOS, Adaption Anschlag |
| 0x2A8B | CDKENWSAD2 - Einlass-VANOS, Adaption Anschlag 2 |
| 0x2A8C | CDKANWSAD - Auslass-VANOS, Adaption Anschlag |
| 0x2A8D | CDKANWSAD2 - Auslass-VANOS, Adaption Anschlag 2 |
| 0x2A8E | CDKNWEKW - Einlassnockenwelle, Zahnversatz zur Kurbelwelle |
| 0x2A8F | CDKNWEKW2 - Einlassnockenwelle 2, Zahnversatz zur Kurbelwelle |
| 0x2A90 | CDKNWAKW - Auslassnockenwelle, Zahnversatz zur Kurbelwelle |
| 0x2A91 | CDKNWAKW2 - Auslassnockenwelle 2, Zahnversatz zur Kurbelwelle |
| 0x2B5C | CDKN - Kurbelwellensensor, Signal |
| 0x2B5D | CDKBM - Kurbelwellensensor, Plausibilität |
| 0x2B62 | CDKPH - Nockenwellensensor, Einlass |
| 0x2B63 | CDKPH2 - Nockenwellensensor, Auslass |
| 0x2B64 | CDKPH3 - Nockenwellensensor 2, Einlass |
| 0x2B65 | CDKPH4 - Nockenwellensensor 2, Auslass |
| 0x2B66 | CDKPHM - Nockenwellensensor, Master |
| 0x2B70 | CDKSUE - Variable Sauganlage, Ansteuerung |
| 0x2B71 | CDKDISA - Variable Sauganlage |
| 0x2B72 | CDKDISAT - Variable Sauganlage, Temperaturwarnschwelle |
| 0x2B73 | CDKDISAPL - Variable Sauganlage, Plausibilität |
| 0x2B80 | CDKLLR - Leerlaufregelung |
| 0x2B82 | CDKLLRKH - Leerlaufregelung bei Katalysatorbeheizung |
| 0x2B98 | CDKNVRMON - Steuergerät, interner Fehler: RAM Backup, Plausibilität |
| 0x2B99 | CDKNVRBUP - Steuergerät, interner Fehler: RAM Backup |
| 0x2B9A | CDKURRAM - Steuergerät, interner Fehler: RAM |
| 0x2B9B | CDKURROM - Steuergerät, interner Fehler: ROM |
| 0x2B9C | CDKURRST - Steuergerät, interner Fehler: Reset |
| 0x2B9D | CDKWDA - Steuergerät, interner Fehler: Überspannung |
| 0x2B9E | CDKFETRWE - Steuergerät, Drehzahlbegrenzung aktiviert |
| 0x2BC0 | CDKTUMP - Umgebungstemperatursensor, Plausibilität |
| 0x2BC1 | CDKTUME - Umgebungstemperatursensor, Signal |
| 0x2C24 | CDKLSVV - Lambdasonden vor Katalysator, vertauscht |
| 0x2C31 | CDKFTDLA - Lambdasonde vor Katalysator, Trimmregelung |
| 0x2C32 | CDKFTDLA2 - Lambdasonde vor Katalysator 2, Trimmregelung |
| 0x2C37 | CDKHELSU - Lambdasonde vor Katalysator, Heizereinkopplung |
| 0x2C38 | CDKHELSU2 - Lambdasonde vor Katalysator 2, Heizereinkopplung |
| 0x2C39 | CDKDYLSU - Lambdasonde vor Katalysator, Dynamik |
| 0x2C3A | CDKDYLSU2 - Lambdasonde vor Katalysator 2, Dynamik |
| 0x2C3B | CDKULSU - Lambdasonde vor Katalysator, nicht angesteckt |
| 0x2C3C | CDKULSU2 - Lambdasonde vor Katalysator 2, nicht angesteckt |
| 0x2C47 | CDKLSUKS - Lambdasonde vor Katalysator, Sondenleitungen |
| 0x2C48 | CDKLSUKS2 - Lambdasonde vor Katalysator 2, Sondenleitungen |
| 0x2C49 | CDKPLLSU - Lambdasonde vor Katalysator, Plausibilität |
| 0x2C4A | CDKPLLSU2 - Lambdasonde vor Katalysator 2, Plausibilität |
| 0x2C4B | CDKICLSU - Steuergerät, interner Fehler: Lambdasondenbaustein |
| 0x2C4C | CDKICLSU2 - Steuergerät, interner Fehler: Lambdasondenbaustein 2 |
| 0x2C4D | CDKLSUIP - Lambdasonde vor Katalysator, Pumpstromleitung |
| 0x2C4E | CDKLSUIP2 - Lambdasonde vor Katalysator 2, Pumpstromleitung |
| 0x2C4F | CDKLSUIA - Lambdasonde vor Katalysator, Abgleichleitung |
| 0x2C50 | CDKLSUIA2 - Lambdasonde vor Katalysator 2, Abgleichleitung |
| 0x2C51 | CDKLSUUN - Lambdasonde vor Katalysator, Nernstleitung |
| 0x2C52 | CDKLSUUN2 - Lambdasonde vor Katalysator 2, Nernstleitung |
| 0x2C53 | CDKLSUVM - Lambdasonde vor Katalysator, virtuelle Masse |
| 0x2C54 | CDKLSUVM2 - Lambdasonde vor Katalysator 2, virtuelle Masse |
| 0x2C61 | CDKLSVE - Lamdasonde vor Katalysator, elektrischer Fehler |
| 0x2C62 | CDKLSVE2 - Lamdasonde vor Katalysator 2, elektrischer Fehler |
| 0x2C6D | CDKLASH - Lambdasonde nach Katalysator, Alterung |
| 0x2C6E | CDKLASH2 - Lambdasonde nach Katalysator 2, Alterung |
| 0x2C71 | CDKLSH - Lambdasonde nach Katalysator |
| 0x2C72 | CDKLSH2 - Lambdasonde nach Katalysator 2 |
| 0x2C84 | CDKDYLSH - Lambdasonde nach Katalysator, Dynamik |
| 0x2C85 | CDKDYLSH2 - Lambdasonde 2 nach Katalysator, Dynamik |
| 0x2C9C | CDKHSVE - Lambdasondenbeheizung vor Katalysator, Ansteuerung |
| 0x2C9D | CDKHSVE2 - Lambdasondenbeheizung vor Katalysator 2, Ansteuerung |
| 0x2C9E | CDKHSHE - Lambdasondenbeheizung nach Katalysator, Ansteuerung |
| 0x2C9F | CDKHSHE2 - Lambdasondenbeheizung nach Katalysator 2, Ansteuerung |
| 0x2CA0 | CDKHSV - Lambdasondenbeheizung vor Katalysator |
| 0x2CA1 | CDKHSV2 - Lambdasondenbeheizung vor Katalysator 2 |
| 0x2CA8 | CDKHSH - Lambdasondenbeheizung nach Katalysator, Funktion |
| 0x2CA9 | CDKHSH2 - Lambdasondenbeheizung nach Katalysator 2, Funktion |
| 0x2CEF | CDKDVEE - Drosselklappensteller, Ansteuerung |
| 0x2CF0 | CDKDVER - Drosselklappensteller, Regelbereich |
| 0x2CF1 | CDKDVEL - Drosselklappensteller, Positionsüberwachung |
| 0x2CF8 | CDKDK - Drosselklappenpotenziometer |
| 0x2CF9 | CDKDK1P - Drosselklappenpotenziometer 1 |
| 0x2CFA | CDKDK2P - Drosselklappenpotenziometer 2 |
| 0x2CFF | CDKDVEV - Drosselklappensteller, Verstärkerabgleich |
| 0x2D00 | CDKDVEF - Drosselklappensteller, Federprüfung schliessende Feder |
| 0x2D01 | CDKDVEFO - Drosselklappensteller, Federprüfung öffnende Feder |
| 0x2D02 | CDKDVEN - Drosselklappensteller, Notluftpunkt |
| 0x2D03 | CDKDVEUB - Drosselklappensteller, Abbruch Adaption wegen Umweltbedingungen |
| 0x2D04 | CDKDVEU - Drosselklappensteller, Prüfung unterer Anschlag |
| 0x2D05 | CDKDVEUW - Drosselklappensteller, Abbruch bei UMA-Wiederlernen |
| 0x2D0F | CDKHFME - Luftmassenmesser, Signal |
| 0x2D14 | CDKKHFME - Luftmassenmesser, Korrektursignal |
| 0x2D1A | CDKFPP - Fahrpedalmodul, Pedalwertgeber |
| 0x2D1B | CDKFP1P - Fahrpedalmodul, Pedalwertgeber Signal 1 |
| 0x2D1C | CDKFP2P - Fahrpedalmodul, Pedalwertgeber Signal 2 |
| 0x2D28 | CDKDDSS - Differenzdrucksensor, Saugrohr: Signal |
| 0x2D29 | CDKPDDSS - Differenzdrucksensor, Saugrohr: Plausibilität |
| 0x2D32 | CDKDPSRPL - Differenzdrucksensor, Saugrohr: Plausibilität |
| 0x2D6E | CDKUFMV - DME, interner Fehler: Überwachung Istmoment |
| 0x2D70 | CDKUFSGA - DME, interner Fehler: Überwachung Motorfunktionen |
| 0x2D71 | CDKUFSGB - DME, interner Fehler: Überwachung Eingangsgrößen |
| 0x2D72 | CDKUFSGC - DME, interner Fehler: Überwachung Hardware |
| 0x2D75 | CDKUFNC - DME, interner Fehler: Überwachung Motordrehzahl |
| 0x2D76 | CDKUFSPSC - DME, interner Fehler: Überwachung Fahrpedalmodul |
| 0x2D78 | CDKUFMSAC - Luftmassenstromabgleich |
| 0x2DBF | CDKCACC - CAN, ACC: Signalfehler |
| 0x2DCA | CDKCEGS - Botschaft vom EGS fehlt, Timeout |
| 0x2DCB | CDKCSSG - CAN, SSG: Signalfehler |
| 0x2DCF | CDKCINS - CAN, Instrumentenkombination: Signalfehler |
| 0x2DD7 | CDKCDSC - Botschaft vom DSC fehlt, Timeout |
| 0x2DD9 | CDKCARS - CAN, ARS: Signalfehler |
| 0x2DDA | CDKCCAS - CAN, CAS: Signalfehler |
| 0x2DDB | CDKCIHKA - CAN, IHKA: Signalfehler |
| 0x2DDC | CDKCSZL - Botschaft vom SZL fehlt |
| 0x2DDD | CDKCVVT - Botschaft vom Valvetronic-Steuergerät fehlt |
| 0x2DDE | CDKDVCAN - Local-CAN Kommunikation |
| 0x2DDF | CDKDVCAN2 - Local-CAN Kommunikation 2 |
| 0x2DEB | CDKPMBN - Powermanagement, Bordnetzüberwachung |
| 0x2DEC | CDKPMBAT - Powermanagement, Batterieüberwachung |
| 0x2DED | CDKPMRUHV - Powermanagement, Ruhestromüberwachung |
| 0x2E24 | CDKDZKU0 - Zündspule Zylinder 1 |
| 0x2E25 | CDKDZKU7 - Zündspule Zylinder 2 |
| 0x2E26 | CDKDZKU5 - Zündspule Zylinder 3 |
| 0x2E27 | CDKDZKU2 - Zündspule Zylinder 4 |
| 0x2E28 | CDKDZKU1 - Zündspule Zylinder 5 |
| 0x2E29 | CDKDZKU4 - Zündspule Zylinder 6 |
| 0x2E2A | CDKDZKU6 - Zündspule Zylinder 7 |
| 0x2E2B | CDKDZKU3 - Zündspule Zylinder 8 |
| 0x2E30 | CDKEV1 - Einspritzventil Zylinder 1, Ansteuerung |
| 0x2E31 | CDKEV8 - Einspritzventil Zylinder 2, Ansteuerung |
| 0x2E32 | CDKEV6 - Einspritzventil Zylinder 3, Ansteuerung |
| 0x2E33 | CDKEV3 - Einspritzventil Zylinder 4, Ansteuerung |
| 0x2E34 | CDKEV2 - Einspritzventil Zylinder 5, Ansteuerung |
| 0x2E35 | CDKEV5 - Einspritzventil Zylinder 6, Ansteuerung |
| 0x2E36 | CDKEV7 - Einspritzventil Zylinder 7, Ansteuerung |
| 0x2E37 | CDKEV4 - Einspritzventil Zylinder 8, Ansteuerung |
| 0x2E68 | CDKKS1 - Klopfsensorsignal 1 |
| 0x2E69 | CDKKS2 - Klopfsensorsignal 2 |
| 0x2E6A | CDKKS3 - Klopfsensorsignal 3 |
| 0x2E6B | CDKKS4 - Klopfsensorsignal 4 |
| 0x2E6E | CDKDZKUB1 - Zündung, Überwachung: Brenndauer |
| 0x2E6F | CDKDZKUB2 - Zündung 2, Überwachung: Brenndauer |
| 0x2E72 | CDKKRIC - Steuergerät, interner Fehler: Klopfsensorbaustein |
| 0x2E73 | CDKKRSPI - Steuergerät, interner Fehler: Klopfsensorbaustein |
| 0x2E7C | CDKBSD - Bitserielle Datenschnittstelle, Signal |
| 0x2E8B | CDKIBSK - Intelligenter Batteriesensor, Signal |
| 0x2E8C | CDKIBSP - Intelligenter Batteriesensor, Funktion |
| 0x2E8D | CDKIBSA - Intelligenter Batteriesensor, Signalübertragung |
| 0x2E97 | CDKGEN - Generator |
| 0x2EA0 | CDKQLT - Ölzustandssensor |
| 0x2EB8 | CDKBSDD0 - BSD-Botschaft vom intelligenten Batteriesensor fehlt |
| 0x2EBA | CDKBSDD2 - BSD-Botschaft von der elektrischen Kühlmittelpumpe, Elektronik fehlt |
| 0x2EBB | CDKBSDD3 - BSD-Botschaft von der elektrischen Kühlmittelpumpe, Motor fehlt |
| 0x2EBC | CDKBSDD4 - BSD-Botschaft vom Ölzustandssensor fehlt |
| 0x2EBD | CDKBSDD6 - BSD-Botschaft vom Generator fehlt |
| 0x2EBE | CDKBSDD5 - BSD-Botschaft vom Generator 2 fehlt |
| 0x2ECC | CDKGENCOM - Generator, Kommunikation |
| 0x2ECD | CDKGENEL - Generator, elektrisch |
| 0x2ECE | CDKGENELB - Generator, Plausibilität: elektrisch |
| 0x2ECF | CDKGENHT - Generator, Übertemperatur |
| 0x2ED0 | CDKGENHTB - Generator,  Plausibilität: Temperatur |
| 0x2ED1 | CDKGENME - Generator, mechanisch |
| 0x2ED2 | CDKGENREG - Generator, Regler falsch |
| 0x2ED3 | CDKGENUPL - Generator, Typ falsch |
| 0x2EE0 | CDKTME - Kühlmitteltemperatursensor, Signal |
| 0x2EE1 | CDKTMP - Kühlmitteltemperatursensor, Plausibilität |
| 0x2EEA | CDKTKAE - Temperatursensor Kühleraustritt, Signal |
| 0x2EEC | CDKTKAR - Temperatursensor Kühleraustritt, Plausibilität |
| 0x2EF4 | CDKTHM - Kennfeldthermostat, Mechanik |
| 0x2EF5 | CDKETS - Kennfeldthermostat, Ansteuerung |
| 0x2EFE | CDKMLE - Elektrolüfter, Ansteuerung |
| 0x2F08 | CDKTAE - Ansauglufttemperatursensor, Signal |
| 0x2F09 | CDKTAR - Ansauglufttemperatursensor, Plausibilität |
| 0x2F0B | CDKTACS - Ansauglufttemperatursensor: Kaltanteil, Plausibilität (vorläufig) |
| 0x2F0D | CDKGLFE - Kühlerjalousie, Ansteuerung, (GLF) |
| 0x2F10 | CDKPKKSFB - Kühlerjalousie, unten |
| 0x2F11 | CDKAKKSFB - Kühlerjalousie, oben |
| 0x2F12 | CDKKOSE - Klimakompressor, Ansteuerung |
| 0x2F17 | CDKMTOEL - Motoröltemperatur, zeitweise zu hoch, EGS-Zwangsschaltung |
| 0x2F44 | CDKWFS - EWS Manipulationsschutz |
| 0x2F45 | CDKDWA - Schnittstelle EWS-DME |
| 0x2F46 | CDKWCA - EWS Wechselcode-Abspeicherng |
| 0x2F4E | CDKVFZE - Fahrzeuggeschwindigkeit, Signal |
| 0x2F4F | CDKVFZNP - Fahrzeuggeschwindigkeit, Plausibilität |
| 0x2F50 | CDKVAT - Fahrzeuggeschwindigkeit, Plausibilität |
| 0x2F59 | CDKSTS - Startautomatik, Startsignal |
| 0x2F5A | CDKSTA - Startautomatik |
| 0x2F62 | CDKBREMS - Bremslichtschalter |
| 0x2F67 | CDKKUPPL - Kupplungsschalter, Signal |
| 0x2F6C | CDKAKRE - Abgasklappe, Ansteuerung |
| 0x2F71 | CDKELS - E-Box-Lüfter, Ansteuerung |
| 0x2F77 | CDKPUR - Umgebungsdrucksensor, Plausibilität |
| 0x2F78 | CDKPUE - DME, interner Fehler: Umgebungsdrucksensor |
| 0x2F7B | CDKPOELS - Öldruckschalter, Plausibilität |
| 0x2F80 | CDKCUHR - Motorabstellzeit, Plausibilität |
| 0x2F8A | CDKUB - Batteriespannung |
| 0x2F94 | CDKKPE - Kraftstoffpumpenrelais, Ansteuerung |
| 0x2F9E | CDKTOENS - Thermischer Ölniveausensor |
| 0x2FA3 | CDKCOD - Codierung fehlt |
| 0xCD87 | CDKCANA - PT-CAN Kommunikationsfehler |
| 0xCD8B | CDKCANB - Local-CAN Kommunikationsfehler |
| 0xCD97 | CDKXB1 - Botschaft (Drehmomentanforderung AFS, B1) |
| 0xCD9B | CDKX315 - Botschaft (Fahrzeugmodus, 315) |
| 0xCDA1 | CDKXC4 - Botschaft (Lenkradwinkel, C4) |
| 0xCDA2 | CDKX3B4 - Botschaft (Powermanagement Batteriespannung, 3B4) |
| 0xCDA3 | CDKX334 - Botschaft (Powermanagement Ladespannung, 334) |
| 0xCDA7 | CDKX3B0 - Botschaft (Status Rückwärtsgang, 3B0) |
| 0xCDAA | CDKX135 - Botschaft (Status Crashabschaltung EKP, 135) |
| 0xCDAC | CDKX3B5 - Botschaft (Status Wasserventil,  3B5) |
| 0xCDB0 | CDKX1D2 - Botschaft (Anzeige Getriebedaten) |
| 0xCDB3 | CDKXB9 - Botschaft (Drehmomentanforderung Lenkung, B9) |
| 0xCDB7 | CDKX5E0 - Botschaft (OBD-Sensor Diagnosestatus, 5E0) |
| 0xCDEB | CDKX21A - Botschaft (Lampenzustand,  21A) |
| 0xCDED | CDKXBF - Botschaft (Anforderung Radmoment Antriebstrang,  BF) |
| 0xCDEE | CDKX2F8 - Botschaft (Uhrzeit/Datum, 2F8) |
| 0xCDEF | CDKX2E4 - Botschaft (Status Anhänger, 2E4) |
| 0xCDF9 | CDKX201 - Botschaft (Status EMF, 201) (vorläufig) |
| 0xCDFA | CDKX1A7 - Botschaft (Stellanforderung EMF, 1A7) (vorläufig) |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | 00654321 |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 12 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxx0 | 10 | -- |
| xxxxxxx1 | 11 | Diagnose aktiv |
| xxxxxx0x | 20 | -- |
| xxxxxx1x | 21 | Diagnose gestoppt |
| xxxxx0xx | 30 | -- |
| xxxxx1xx | 31 | Zyklus-Flag gesetzt |
| xxxx0xxx | 40 | -- |
| xxxx1xxx | 41 | Error-Flag gesetzt |
| xxx0xxxx | 50 | -- |
| xxx1xxxx | 51 | MIL ein |
| xx0xxxxx | 60 | -- |
| xx1xxxxx | 61 | Fehler in Entprellphase |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 277 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x0000 | 0x00FF | 0x00FF | 0x00FF | 0x00FF |
| 0x29CC | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29CD | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29CE | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29CF | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29D0 | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29D1 | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29D2 | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29D3 | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29D4 | 0x000A | 0x001A | 0x0012 | 0x003C |
| 0x29D9 | 0x003C | 0x0005 | 0x00B2 | 0x00B3 |
| 0x29DD | 0x000A | 0x001A | 0x000B | 0x008C |
| 0x29E5 | 0x000B | 0x001A | 0x0008 | 0x0006 |
| 0x29E6 | 0x000B | 0x001A | 0x0006 | 0x0008 |
| 0x29E7 | 0x000A | 0x0013 | 0x003C | 0x0005 |
| 0x29E8 | 0x000A | 0x0013 | 0x003C | 0x0007 |
| 0x29ED | 0x000A | 0x001A | 0x00AD | 0x00AC |
| 0x29EE | 0x000B | 0x001A | 0x00AD | 0x00AC |
| 0x29EF | 0x0005 | 0x0006 | 0x001A | 0x000A |
| 0x29F0 | 0x0007 | 0x0008 | 0x001A | 0x000A |
| 0x29F4 | 0x00A3 | 0x001A | 0x00BF | 0x00C1 |
| 0x29F5 | 0x00A4 | 0x001A | 0x00C0 | 0x00C2 |
| 0x29FA | 0x000A | 0x002B | 0x0014 | 0x00A5 |
| 0x2A12 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A13 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A14 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A15 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A16 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A17 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A18 | 0x000A | 0x0014 | 0x0024 | 0x000B |
| 0x2A19 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A1A | 0x000A | 0x001A | 0x0024 | 0x0035 |
| 0x2A1D | 0x000A | 0x003C | 0x0014 | 0x000B |
| 0x2A1E | 0x000A | 0x003C | 0x0014 | 0x000B |
| 0x2A58 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A59 | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A5A | 0x000A | 0x0014 | 0x0012 | 0x00C6 |
| 0x2A5B | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A5C | 0x000A | 0x0014 | 0x0012 | 0x00C6 |
| 0x2A5D | 0x000A | 0x0014 | 0x0012 | 0x00C3 |
| 0x2A5E | 0x000A | 0x0014 | 0x0012 | 0x00C4 |
| 0x2A5F | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A60 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A61 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A62 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A63 | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A64 | 0x000A | 0x0014 | 0x0012 | 0x00C6 |
| 0x2A65 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A66 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A67 | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A68 | 0x000A | 0x0014 | 0x0012 | 0x00C6 |
| 0x2A69 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A6A | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A6B | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A6C | 0x000A | 0x0014 | 0x0012 | 0x00BE |
| 0x2A6D | 0x000A | 0x008C | 0x0012 | 0x00C5 |
| 0x2A6E | 0x000A | 0x008C | 0x0012 | 0x00C6 |
| 0x2A6F | 0x0012 | 0x00BE | 0x000A | 0x001A |
| 0x2A80 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A81 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A83 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A84 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A85 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A86 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A88 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A89 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8A | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8B | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8C | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8D | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8E | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8F | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A90 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A91 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2B5C | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B5D | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B62 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B63 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B64 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B65 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B66 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B70 | 0x000A | 0x0012 | 0x0013 | 0x0023 |
| 0x2B71 | 0x0012 | 0x000A | 0x0013 | 0x0023 |
| 0x2B72 | 0x0012 | 0x000A | 0x0013 | 0x0023 |
| 0x2B73 | 0x0012 | 0x000A | 0x0013 | 0x0023 |
| 0x2B80 | 0x000A | 0x001A | 0x0014 | 0x0015 |
| 0x2B82 | 0x000A | 0x001A | 0x0014 | 0x0015 |
| 0x2B98 | 0x0014 | 0x00BE | 0x0012 | 0x0024 |
| 0x2B99 | 0x000A | 0x0014 | 0x0012 | 0x00BE |
| 0x2B9A | 0x000A | 0x001A | 0x001F | 0x0022 |
| 0x2B9B | 0x000A | 0x001A | 0x001F | 0x0022 |
| 0x2B9C | 0x000A | 0x001A | 0x001F | 0x0022 |
| 0x2B9D | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2B9E | 0x0014 | 0x00BE | 0x00FF | 0x00FF |
| 0x2BC0 | 0x0012 | 0x0013 | 0x0024 | 0x0014 |
| 0x2BC1 | 0x0012 | 0x0013 | 0x0024 | 0x0014 |
| 0x2C24 | 0x0012 | 0x008C | 0x00A8 | 0x00A9 |
| 0x2C31 | 0x009D | 0x00A8 | 0x0017 | 0x0085 |
| 0x2C32 | 0x009E | 0x00A9 | 0x0019 | 0x0086 |
| 0x2C37 | 0x0082 | 0x00A8 | 0x0029 | 0x003C |
| 0x2C38 | 0x0083 | 0x00A9 | 0x002A | 0x003C |
| 0x2C39 | 0x00AA | 0x00B0 | 0x00A8 | 0x0085 |
| 0x2C3A | 0x00AB | 0x00B1 | 0x00A9 | 0x0086 |
| 0x2C3B | 0x008C | 0x00A8 | 0x0017 | 0x0044 |
| 0x2C3C | 0x008C | 0x00A9 | 0x0019 | 0x0045 |
| 0x2C47 | 0x0014 | 0x000B | 0x00A8 | 0x009F |
| 0x2C48 | 0x0014 | 0x000B | 0x00A9 | 0x00A0 |
| 0x2C49 | 0x009D | 0x00A8 | 0x0017 | 0x0085 |
| 0x2C4A | 0x009E | 0x00A9 | 0x0019 | 0x0086 |
| 0x2C4B | 0x009F | 0x008C | 0x0014 | 0x00A8 |
| 0x2C4C | 0x00A0 | 0x008C | 0x0014 | 0x00A9 |
| 0x2C4D | 0x00A8 | 0x0082 | 0x0044 | 0x009F |
| 0x2C4E | 0x00A9 | 0x0083 | 0x0045 | 0x00A0 |
| 0x2C4F | 0x00A8 | 0x0082 | 0x0044 | 0x008C |
| 0x2C50 | 0x00A9 | 0x0083 | 0x0045 | 0x008C |
| 0x2C51 | 0x00A8 | 0x0082 | 0x0044 | 0x009F |
| 0x2C52 | 0x00A9 | 0x0083 | 0x0045 | 0x00A0 |
| 0x2C53 | 0x0014 | 0x00A8 | 0x0082 | 0x009F |
| 0x2C54 | 0x0014 | 0x00A9 | 0x0083 | 0x00A0 |
| 0x2C61 | 0x0029 | 0x0044 | 0x00A8 | 0x000B |
| 0x2C62 | 0x002A | 0x0045 | 0x00A9 | 0x000B |
| 0x2C6D | 0x000A | 0x002B | 0x0033 | 0x0017 |
| 0x2C6E | 0x000A | 0x002C | 0x0034 | 0x0019 |
| 0x2C71 | 0x002B | 0x008C | 0x0033 | 0x0017 |
| 0x2C72 | 0x002C | 0x008C | 0x0034 | 0x0019 |
| 0x2C84 | 0x002B | 0x008C | 0x0033 | 0x0017 |
| 0x2C85 | 0x002C | 0x008C | 0x0034 | 0x0019 |
| 0x2C9C | 0x000B | 0x008C | 0x0014 | 0x0044 |
| 0x2C9D | 0x000B | 0x008C | 0x0014 | 0x0045 |
| 0x2C9E | 0x000A | 0x0012 | 0x0013 | 0x0014 |
| 0x2C9F | 0x000A | 0x0012 | 0x0013 | 0x0014 |
| 0x2CA0 | 0x000B | 0x008C | 0x0029 | 0x0044 |
| 0x2CA1 | 0x000B | 0x008C | 0x002A | 0x0045 |
| 0x2CA8 | 0x007E | 0x0017 | 0x002B | 0x0033 |
| 0x2CA9 | 0x007F | 0x0019 | 0x002C | 0x0034 |
| 0x2CEF | 0x0014 | 0x0012 | 0x0015 | 0x0028 |
| 0x2CF0 | 0x0014 | 0x0013 | 0x0015 | 0x0028 |
| 0x2CF1 | 0x0014 | 0x0013 | 0x0015 | 0x0028 |
| 0x2CF8 | 0x000A | 0x0015 | 0x0026 | 0x0027 |
| 0x2CF9 | 0x000A | 0x0028 | 0x0024 | 0x0027 |
| 0x2CFA | 0x000A | 0x0028 | 0x0024 | 0x0026 |
| 0x2CFF | 0x0014 | 0x0013 | 0x0026 | 0x0065 |
| 0x2D00 | 0x0014 | 0x0013 | 0x0015 | 0x0064 |
| 0x2D01 | 0x0014 | 0x0013 | 0x0015 | 0x0064 |
| 0x2D02 | 0x0014 | 0x0013 | 0x0064 | 0x00FF |
| 0x2D03 | 0x000A | 0x0014 | 0x0013 | 0x0023 |
| 0x2D04 | 0x0014 | 0x0013 | 0x0026 | 0x0065 |
| 0x2D05 | 0x000A | 0x0014 | 0x0013 | 0x0023 |
| 0x2D0F | 0x000A | 0x0012 | 0x0014 | 0x001A |
| 0x2D14 | 0x000A | 0x0012 | 0x0014 | 0x001A |
| 0x2D1A | 0x000A | 0x0023 | 0x001B | 0x001D |
| 0x2D1B | 0x000A | 0x0023 | 0x001B | 0x001D |
| 0x2D1C | 0x000A | 0x0023 | 0x001B | 0x001D |
| 0x2D28 | 0x000A | 0x001A | 0x0012 | 0x0014 |
| 0x2D29 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2D32 | 0x000A | 0x0013 | 0x0015 | 0x00FF |
| 0x2D6E | 0x000A | 0x001A | 0x0020 | 0x0021 |
| 0x2D70 | 0x0014 | 0x0013 | 0x000A | 0x0012 |
| 0x2D71 | 0x0014 | 0x0013 | 0x000A | 0x0012 |
| 0x2D72 | 0x0014 | 0x0013 | 0x000A | 0x0012 |
| 0x2D75 | 0x000A | 0x0015 | 0x001F | 0x0023 |
| 0x2D76 | 0x001B | 0x001C | 0x0023 | 0x001F |
| 0x2D78 | 0x0011 | 0x000A | 0x0015 | 0x0014 |
| 0x2DBF | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DCA | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DCB | 0x000A | 0x001A | 0x0014 | 0x00C9 |
| 0x2DCF | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DD7 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DD9 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDA | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDB | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDC | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDD | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDE | 0x000A | 0x0014 | 0x0012 | 0x008C |
| 0x2DDF | 0x000A | 0x0014 | 0x0012 | 0x008C |
| 0x2DEB | 0x00DF | 0x00BA | 0x000A | 0x00BC |
| 0x2DEC | 0x00DD | 0x00DE | 0x00DF | 0x00A5 |
| 0x2DED | 0x00FB | 0x00FC | 0x00FD | 0x00BE |
| 0x2E24 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E25 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E26 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E27 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E28 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E29 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2A | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2B | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E30 | 0x000A | 0x0012 | 0x0014 | 0x0005 |
| 0x2E31 | 0x000A | 0x0012 | 0x0014 | 0x0005 |
| 0x2E32 | 0x000A | 0x0012 | 0x0014 | 0x0005 |
| 0x2E33 | 0x000A | 0x0012 | 0x0014 | 0x0005 |
| 0x2E34 | 0x000A | 0x0012 | 0x0014 | 0x0007 |
| 0x2E35 | 0x000A | 0x0012 | 0x0014 | 0x0007 |
| 0x2E36 | 0x000A | 0x0012 | 0x0014 | 0x0007 |
| 0x2E37 | 0x000A | 0x0012 | 0x0014 | 0x0007 |
| 0x2E68 | 0x000A | 0x001A | 0x008D | 0x0094 |
| 0x2E69 | 0x000A | 0x001A | 0x0092 | 0x008F |
| 0x2E6A | 0x000A | 0x001A | 0x008E | 0x0091 |
| 0x2E6B | 0x000A | 0x001A | 0x0093 | 0x0090 |
| 0x2E6E | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E6F | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E72 | 0x000A | 0x001A | 0x0080 | 0x00FF |
| 0x2E73 | 0x000A | 0x001A | 0x0080 | 0x00FF |
| 0x2E7C | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2E8B | 0x00D4 | 0x00D5 | 0x000A | 0x0014 |
| 0x2E8C | 0x00D4 | 0x00D5 | 0x000A | 0x0014 |
| 0x2E8D | 0x00D4 | 0x00D5 | 0x000A | 0x0014 |
| 0x2E97 | 0x004B | 0x00FA | 0x00BA | 0x0014 |
| 0x2EA0 | 0x000A | 0x00E1 | 0x0014 | 0x00FF |
| 0x2EB8 | 0x00D4 | 0x00D5 | 0x0014 | 0x008C |
| 0x2EBA | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2EBB | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2EBC | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2EBD | 0x008C | 0x0054 | 0x0048 | 0x0014 |
| 0x2EBE | 0x008C | 0x0054 | 0x0048 | 0x0014 |
| 0x2ECC | 0x008C | 0x0054 | 0x0048 | 0x0014 |
| 0x2ECD | 0x00F8 | 0x00FA | 0x00F9 | 0x0014 |
| 0x2ECE | 0x00F8 | 0x00FA | 0x00F9 | 0x0014 |
| 0x2ECF | 0x004B | 0x00FA | 0x00F8 | 0x0014 |
| 0x2ED0 | 0x004B | 0x00FA | 0x00F8 | 0x004A |
| 0x2ED1 | 0x008C | 0x00FA | 0x00F9 | 0x0014 |
| 0x2ED2 | 0x0049 | 0x0054 | 0x0048 | 0x0014 |
| 0x2ED3 | 0x008C | 0x0054 | 0x0048 | 0x0014 |
| 0x2EE0 | 0x0025 | 0x0013 | 0x000A | 0x0072 |
| 0x2EE1 | 0x0025 | 0x0013 | 0x000A | 0x0072 |
| 0x2EEA | 0x000A | 0x0012 | 0x0024 | 0x0074 |
| 0x2EEC | 0x000A | 0x0012 | 0x0024 | 0x0074 |
| 0x2EF4 | 0x000A | 0x0012 | 0x0024 | 0x0074 |
| 0x2EF5 | 0x000A | 0x0012 | 0x0013 | 0x0014 |
| 0x2EFE | 0x000A | 0x0012 | 0x0014 | 0x006B |
| 0x2F08 | 0x000A | 0x0012 | 0x0024 | 0x0073 |
| 0x2F09 | 0x000A | 0x0012 | 0x0024 | 0x0073 |
| 0x2F0B | 0x000A | 0x0012 | 0x0024 | 0x0073 |
| 0x2F0D | 0x000A | 0x0012 | 0x0013 | 0x0014 |
| 0x2F10 | 0x0014 | 0x0024 | 0x0047 | 0x0046 |
| 0x2F11 | 0x0014 | 0x0024 | 0x0047 | 0x0046 |
| 0x2F12 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2F17 | 0x000A | 0x0012 | 0x0013 | 0x0014 |
| 0x2F44 | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2F45 | 0x000A | 0x0012 | 0x0014 | 0x00BE |
| 0x2F46 | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2F4E | 0x000A | 0x001A | 0x00CB | 0x0014 |
| 0x2F4F | 0x000A | 0x001A | 0x00CB | 0x0014 |
| 0x2F50 | 0x000A | 0x001A | 0x00CB | 0x0014 |
| 0x2F59 | 0x000A | 0x0014 | 0x0012 | 0x008C |
| 0x2F5A | 0x000A | 0x001A | 0x0014 | 0x000B |
| 0x2F62 | 0x000A | 0x0012 | 0x000B | 0x0014 |
| 0x2F67 | 0x000A | 0x0012 | 0x000B | 0x0014 |
| 0x2F6C | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2F71 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2F77 | 0x000A | 0x000B | 0x0024 | 0x0075 |
| 0x2F78 | 0x000A | 0x000B | 0x0024 | 0x0075 |
| 0x2F7B | 0x000A | 0x0012 | 0x001A | 0x008C |
| 0x2F80 | 0x0014 | 0x0024 | 0x00A5 | 0x008C |
| 0x2F8A | 0x000A | 0x0014 | 0x0024 | 0x0012 |
| 0x2F94 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2F9E | 0x000A | 0x00E1 | 0x0014 | 0x00FF |
| 0x2FA3 | 0x0014 | 0x000A | 0x008C | 0x00BE |
| 0xCD87 | 0x000A | 0x0014 | 0x0013 | 0x000B |
| 0xCD8B | 0x000A | 0x0014 | 0x0013 | 0x000B |
| 0xCD97 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCD9B | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDA1 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDA2 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDA3 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDA7 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDAA | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDAC | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDB0 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDB3 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDB7 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDEB | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDED | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDEE | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDEF | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDF9 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDFA | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xFFFF | 0x00FF | 0x00FF | 0x00FF | 0x00FF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 163 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | Regelstatus Bank 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0002 | Regelstatus Bank 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0003 | Relative Luftmasse | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0004 | Motortemperatur | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x0005 | Regelfaktor Bank 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x0006 | Adaptionsfaktor Bank 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x0007 | Regelfaktor Bank 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x0008 | Adaptionsfaktor Bank 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x000A | Motordrehzahl | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x000B | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0011 | Luftmassenfluß | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x0012 | Motortemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0013 | Ansauglufttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0014 | Batteriespannung | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x0015 | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | - | unsigned char | - | 0,39215686917305 | 1 | 0,0 |
| 0x0017 | Sondenspannung hinter Katalysator Bank 1 | V | - | unsigned char | - | 0,00521568628028035 | 1 | -0,2 |
| 0x0019 | Sondenspannung hinter Katalysator Bank 2 | V | - | unsigned char | - | 0,00521568628028035 | 1 | -0,2 |
| 0x001A | relative Luftfüllung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x001B | Spannung Pedalwertgeber Poti 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x001C | Spannung Pedalwertgeber Poti 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x001D | Verdoppelte Spannung Pedalwertgeber Poti 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x001E | Pfadidentifier SKA-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x001F | Pfadidentifier EGAS-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0020 | Pfadidentifier Momenten-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0021 | Istmoment beim Momentenvergleich | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0022 | Pfadidentifier Reset-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0023 | normierter Fahrpedalwinkel | %PED | - | unsigned char | - | 0,39215686917305 | 1 | 0,0 |
| 0x0024 | Umgebungstemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0025 |  Motortemperatur Ersatzwert aus Modell | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0026 | Spannung Drosselklappenpotenziometer 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0027 | Spannung Drosselklappenpotenziometer 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0028 | Sollwert DK-Winkel bez. auf unteren Anschlag | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0029 | Abgastemperatur vor Katalysator aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x002A | Abgastemperatur vor Katalysator aus Modell Bank 2 | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x002B | Katalysatortemperatur aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x002C | Katalysatortemperatur aus Modell Bank 2 | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x0033 | Innenwiderstand Lambdasonde hinter Kat. | Ohm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x0034 | Innenwiderstand Lambdasonde hinter Kat. Bank 2 | Ohm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x0035 | Umgebungsdruck | hPa | - | unsigned char | - | 5,0 | 1 | 0,0 |
| 0x003C | Tankfüllstand 1L / Ink. | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x003E | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x003F | Motortemperatur-Referenzwert aus Modell | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0040 | Berechnetes Ist-Moment in der Funktionsüberwachung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0041 | Ist Gang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0042 | Zulässiges indiziertes Moment vor Filter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0043 | Indiziertes Sollmoment für ZW-Eingriff vor Momentenbegrenzung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0044 | Innenwiderstand LSU | Ohm | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x0045 | Innenwiderstand LSU, Bank 2 | Ohm | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x0046 | Status Luftklappensystem Low Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0047 | Status Luftklappensystem High Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0048 | Kennung Generatortyp und Hersteller Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0049 | Reglerversion on Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x004A | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x004B | Chiptemperatur Generator 1 | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x0054 | Kennung Generator Hersteller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0064 | DK-Winkel der Notluftposition | % | - | unsigned char | - | 0,390630960464478 | 1 | 0,0 |
| 0x0065 | Spannung Drosselklappen-Poti 1 am unteren Anschlag | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0069 | Spannung Lambdasonde hinter Katalysator | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x006A | Spannung Lambdasonde hinter Katalysator 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x006B | Tastverhältnis Elektrolüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x006C | Istwinkel für Einlass-Nockenwelle | Grad KW | - | signed char | - | 1,0 | 1 | 0,0 |
| 0x006D | Istwinkel für Einlass-Nockenwelle Bank 2 | Grad KW | - | signed char | - | 1,0 | 1 | 0,0 |
| 0x006E | Abgleich DK Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x006F | Abgleich DK Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x0072 | ADC- Spannung Motortemperatur | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0073 | ADC- Spannung Ansauglufttemperatur | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0074 | ADC- Spannung Temperaturkuehleraustritt | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0075 | ADC- Spannung Umgebungsdrucksensor | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0077 | Integratorwert Klopfregelung Meßfensterende Testimpuls | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0078 | gefilterte Katalysatortemperatur aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x0079 | gefilterte Katalysatortemperatur aus Modell, Bank2 | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x007E | normierte Heizleistung der Lambdasonde hinter Kat | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x007F | normierte Heizleistung der Lambdasonde hinter Kat 2 | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x0080 | Integratorgradient für Nulltest-Diagnose Klopfregelung | V/s | - | signed char | - | 23,841869354248 | 1 | 0,0 |
| 0x0082 | Lambda-Sollwert bez. auf Einbauort Lambdasonde | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x0083 | Lambda-Sollwert bez. auf Einbauort Lambdasonde Bank 2 | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x0084 | Motorstarttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0085 | schneller Mittelwert des Lambdaregelfaktors | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x0086 | schneller Mittelwert des Lambdaregelfaktors Bank2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x008B | Faktor Luftdichte f(Ansauglufttemp., Höhe) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x008C | Zeit nach Startende | s | - | unsigned char | - | 25,6000003814697 | 1 | 0,0 |
| 0x008D | normierter Referenzpegel KR SW- Zylinder 0 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x008E | normierter Referenzpegel KR SW- Zylinder 1 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x008F | normierter Referenzpegel KR SW- Zylinder 2 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0090 | normierter Referenzpegel KR SW- Zylinder 3 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0091 | normierter Referenzpegel KR SW- Zylinder 4 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0092 | normierter Referenzpegel KR SW- Zylinder 5 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0093 | normierter Referenzpegel KR SW- Zylinder 6 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0094 | normierter Referenzpegel KR SW- Zylinder 7 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0095 | Statusflag ti- Abschaltung bei kat. schädigenden Aussetzerraten | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0096 | Tankfüllstand | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0097 | DMTL Pumpenstrom Referenzleck | mA | - | unsigned char | - | 0,1953125 | 1 | 0,0 |
| 0x0098 | aktuelle Zeit DMTL Leckmessung | s | - | unsigned char | - | 1,60000002384186 | 1 | 0,0 |
| 0x0099 | Abgleich EV Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x009A | Differenz Pumpstrom zwischen Referenz und min. bei Grobleckmessung | mA | - | unsigned char | - | 0,1953125 | 1 | 0,0 |
| 0x009B | Abgleich EV Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x009D | I-Anteil der stetigen LRHK | - | - | signed char | - | 4,8828125E-4 | 1 | 0,0 |
| 0x009E | I-Anteil der stetigen LRHK Bank 2 | - | - | signed char | - | 4,8828125E-4 | 1 | 0,0 |
| 0x009F | Korrekturwert der LSU-Spannung vor Katalysator | V | - | signed char | - | 0,001953125 | 1 | 0,0 |
| 0x00A0 | Korrekturwert der LSU-Spannung vor Katalysator Bank 2 | V | - | signed char | - | 0,001953125 | 1 | 0,0 |
| 0x00A3 | Abgasmassenfluß gefiltert, Bank 1 | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x00A4 | Abgasmassenfluß gefiltert, Bank 2 | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x00A5 | Abstellzeit | s | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x00A6 | LSU-Spannung vor Katalysator, korrigiert (Byte) | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x00A7 | LSU-Spannung vor Katalysator, korrigiert Bank2 (Byte) | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x00A8 | Sondenspannung vor Katalysator einer Breitbandlambdasonde (ADC-Wert) (Byte) | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x00A9 | Sondenspannung vor Katalysator einer Breitbandlambdasonde Bank2 (ADC-Wert) (Byte) | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x00AA | Dynamikwert der LSU | - | - | unsigned char | - | 0,015625 | 1 | 0,0 |
| 0x00AB | Dynamikwert der LSU Bank 2 | - | - | unsigned char | - | 0,015625 | 1 | 0,0 |
| 0x00AC | multiplikativer Gemischadaptionsfaktor unterer multiplikativer Bereich | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x00AD | multiplikativer Gemischadaptionsfaktor unterer multiplikativer Bereich der Bank 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x00AE | Regelabweichung Lambda | - | - | signed char | - | 0,0078125 | 1 | 0,0 |
| 0x00AF | Regelabweichung Lambda Bank 2 | - | - | signed char | - | 0,0078125 | 1 | 0,0 |
| 0x00B0 | Lambdaamplitude nach Filterung | - | - | signed char | - | 0,0625 | 1 | 0,0 |
| 0x00B1 | Lambdaamplitude nach Filterung Bank 2 | - | - | signed char | - | 0,0625 | 1 | 0,0 |
| 0x00B2 | Lambda-Istwert | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00B3 | Lambda-Istwert Bank 2 | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00B4 | Absolutdruck Abgassystem | hPa | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x00B5 | Absolutdruck Abgassystem 2  | hPa | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x00BA | Generatorspannung | V | - | unsigned char | - | 0,100000001490116 | 1 | 10,6 |
| 0x00BB | vom Generator empfangenes Lastsignal | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x00BC | Generatortemperatur | Grad C | - | unsigned char | - | 192,0 | 1 | -48,0 |
| 0x00BD | Beladung des Aktivkohlefilters | - | - | signed char | - | 0,5 | 1 | 0,0 |
| 0x00BE | Betriebszeit | min | - | unsigned char | - | 1536,0 | 1 | 0,0 |
| 0x00BF | Abgastemperatur im Katalysator aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x00C0 | Abgastemperatur im Katalysator aus Modell Bank 2 | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x00C1 | Istwert Lambdasonde, korrigiert um Zusatzamplitude | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00C2 | Istwert Lambdasonde, korrigiert um Zusatzamplitude, Bank 2 | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00C3 | VVT-Sollwert in Prozent bezüglich Verstellbereich Bank1 | % | - | unsigned char | - | 0,390625089406967 | 1 | 0,0 |
| 0x00C4 | VVT-Sollwert in Prozent bezüglich Verstellbereich Bank 2 | % | - | unsigned char | - | 0,390625089406967 | 1 | 0,0 |
| 0x00C5 | VVT-Istwert in Prozent bezüglich Verstellbereich Bank1 | % | - | unsigned char | - | 0,390625089406967 | 1 | 0,0 |
| 0x00C6 | VVT-Istwert in Prozent bezüglich Verstellbereich Bank2 | % | - | unsigned char | - | 0,390625089406967 | 1 | 0,0 |
| 0x00C7 | Betriebsartenbyte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00C8 | Delta Counter NVRAM-Backup | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00C9 | Status SMG-Diagnose | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00CA | Korrekturfaktor Höhe (byte) | - | - | unsigned char | - | 0,015625 | 1 | 0,0 |
| 0x00CB | Fahrzeuggeschwindigkeit, CAN-Signal | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00CC | schneller Mittelwert des Lambdaregelfaktors | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x00CD | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00CE | Korrekturfaktor Höhe | - | - | unsigned char | - | 0,015625 | 1 | 0,0 |
| 0x00CF | Motorstarttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x00D0 | schneller Mittelwert des Lambdaregelfaktors | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x00D1 | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00D2 | Korrekturfaktor Höhe | - | - | unsigned char | - | 0,015625 | 1 | 0,0 |
| 0x00D3 | Motorstarttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x00D4 | intelligenter Batteriesensor Fehler 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00D5 | intelligenter Batteriesensor Fehler 2 | - | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x00D6 | Referenzmoment für Aussetzererkennung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x00D9 | relative Kraftstoffmasse | % | - | unsigned char | - | 3,0 | 1 | 0,0 |
| 0x00DA | O2- Überschuss bzw. O2-Mangel der LSU im Abgas | % O2 | - | signed char | - | 0,25 | 1 | 0,0 |
| 0x00DB | Korrekturwert für den Innenwiderstand der Nernstzelle der LSU (Byte) | Ohm | - | signed char | - | 10,0 | 1 | 0,0 |
| 0x00DC | Korrekturfaktor für Funktionspumstrom LSU aus Schubabgleich | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x00DD | Status Standverbraucher registriert Teil 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00DE | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00DF | aktuelle Batteriespannung | V | - | unsigned char | - | 0,0640000030398369 | 1 | 6,0 |
| 0x00E1 | relativer Fuellstand des Motoroels | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00F8 | Erregerstrom Generator | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x00F9 | vom Generator empfangene Generatorsollspannung | V | - | unsigned char | - | 0,100000001490116 | 1 | 10,6 |
| 0x00FA | Auslastungsgrad Generator | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x00FB | Verweildauer des Ruhestroms innerhalb 80-200mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x00FC | Verweildauer des Ruhestroms innerhalb 200-1000mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x00FD | Verweildauer des Ruhestroms grösser 1000mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x00FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 275 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x29CC | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29CD | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29CE | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29CF | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D0 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D1 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D2 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D3 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D4 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D9 | 0x0000 | 0x0000 | 0x11EB | 0x0000 |
| 0x29DD | 0x0000 | 0x1116 | 0x0000 | 0x1117 |
| 0x29E5 | 0x0000 | 0x0000 | 0x11EC | 0x11ED |
| 0x29E6 | 0x0000 | 0x0000 | 0x11EC | 0x11ED |
| 0x29E7 | 0x0000 | 0x0000 | 0x11EE | 0x111D |
| 0x29E8 | 0x0000 | 0x0000 | 0x11EE | 0x111D |
| 0x29ED | 0x0000 | 0x0000 | 0x11EF | 0x11F0 |
| 0x29EE | 0x0000 | 0x0000 | 0x11EF | 0x11F0 |
| 0x29EF | 0x11F1 | 0x11F2 | 0x11F4 | 0x11F3 |
| 0x29F0 | 0x11F1 | 0x11F2 | 0x11F4 | 0x11F3 |
| 0x29F4 | 0x0000 | 0x0000 | 0x11F5 | 0x0000 |
| 0x29F5 | 0x0000 | 0x0000 | 0x11F5 | 0x0000 |
| 0x29FA | 0x0000 | 0x0000 | 0x0000 | 0x13B6 |
| 0x2A12 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A13 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A14 | 0x0000 | 0x0000 | 0x0000 | 0x1120 |
| 0x2A15 | 0x0000 | 0x0000 | 0x0000 | 0x1121 |
| 0x2A16 | 0x0000 | 0x0000 | 0x11F6 | 0x0000 |
| 0x2A17 | 0x101D | 0x101E | 0x101F | 0x101C |
| 0x2A18 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A19 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A1A | 0x0000 | 0x0000 | 0x1123 | 0x0000 |
| 0x2A1D | 0x1124 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A1E | 0x0000 | 0x13C5 | 0x1015 | 0x1060 |
| 0x2A58 | 0x0000 | 0x1016 | 0x11F8 | 0x11F9 |
| 0x2A59 | 0x11FA | 0x112A | 0x1127 | 0x1126 |
| 0x2A5A | 0x11FA | 0x112A | 0x1127 | 0x1126 |
| 0x2A5B | 0x11FA | 0x112A | 0x1127 | 0x1126 |
| 0x2A5C | 0x11FA | 0x112A | 0x1127 | 0x1126 |
| 0x2A5D | 0x1028 | 0x11FB | 0x0000 | 0x0000 |
| 0x2A5E | 0x1028 | 0x11FB | 0x0000 | 0x0000 |
| 0x2A5F | 0x0000 | 0x0000 | 0x112B | 0x112C |
| 0x2A60 | 0x0000 | 0x0000 | 0x112B | 0x112C |
| 0x2A61 | 0x0000 | 0x102A | 0x112D | 0x112E |
| 0x2A62 | 0x0000 | 0x102A | 0x112D | 0x112E |
| 0x2A63 | 0x112F | 0x1029 | 0x0000 | 0x0000 |
| 0x2A64 | 0x112F | 0x1029 | 0x0000 | 0x0000 |
| 0x2A65 | 0x1130 | 0x1132 | 0x1133 | 0x1131 |
| 0x2A66 | 0x1130 | 0x11FC | 0x1133 | 0x1131 |
| 0x2A67 | 0x1134 | 0x102F | 0x1015 | 0x1014 |
| 0x2A68 | 0x1134 | 0x102F | 0x1015 | 0x1014 |
| 0x2A69 | 0x102E | 0x0000 | 0x1135 | 0x1136 |
| 0x2A6A | 0x102E | 0x0000 | 0x1135 | 0x1136 |
| 0x2A6B | 0x0000 | 0x11FD | 0x1039 | 0x1138 |
| 0x2A6C | 0x0000 | 0x0000 | 0x0000 | 0x1139 |
| 0x2A6D | 0x11FF | 0x113D | 0x113C | 0x11FE |
| 0x2A6E | 0x11FF | 0x113D | 0x113C | 0x11FE |
| 0x2A6F | 0x0000 | 0x0000 | 0x0000 | 0x113E |
| 0x2A80 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A81 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A83 | 0x1200 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A84 | 0x1200 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A85 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A86 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A88 | 0x1201 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A89 | 0x1201 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A8A | 0x0000 | 0x0000 | 0x1141 | 0x0000 |
| 0x2A8B | 0x0000 | 0x0000 | 0x1141 | 0x0000 |
| 0x2A8C | 0x0000 | 0x0000 | 0x1202 | 0x0000 |
| 0x2A8D | 0x0000 | 0x0000 | 0x1202 | 0x0000 |
| 0x2A8E | 0x0000 | 0x0000 | 0x1143 | 0x0000 |
| 0x2A8F | 0x0000 | 0x0000 | 0x1143 | 0x0000 |
| 0x2A90 | 0x0000 | 0x0000 | 0x1143 | 0x0000 |
| 0x2A91 | 0x0000 | 0x0000 | 0x1143 | 0x0000 |
| 0x2B5C | 0x1203 | 0x1144 | 0x0000 | 0x0000 |
| 0x2B5D | 0x1204 | 0x1146 | 0x0000 | 0x1147 |
| 0x2B62 | 0x1148 | 0x1149 | 0x1015 | 0x1060 |
| 0x2B63 | 0x1148 | 0x1149 | 0x1015 | 0x1060 |
| 0x2B64 | 0x1148 | 0x1149 | 0x1015 | 0x1060 |
| 0x2B65 | 0x1148 | 0x1149 | 0x1015 | 0x1060 |
| 0x2B66 | 0x0000 | 0x1205 | 0x0000 | 0x0000 |
| 0x2B70 | 0x1206 | 0x0000 | 0x1015 | 0x1014 |
| 0x2B71 | 0x1207 | 0x1208 | 0x120A | 0x1209 |
| 0x2B72 | 0x0000 | 0x0000 | 0x120B | 0x0000 |
| 0x2B73 | 0x0000 | 0x0000 | 0x120C | 0x120D |
| 0x2B80 | 0x0000 | 0x0000 | 0x13B8 | 0x13B7 |
| 0x2B82 | 0x0000 | 0x0000 | 0x13B8 | 0x13B7 |
| 0x2B98 | 0x1151 | 0x0000 | 0x0000 | 0x0000 |
| 0x2B99 | 0x0000 | 0x0000 | 0x1210 | 0x1211 |
| 0x2B9A | 0x1154 | 0x0000 | 0x0000 | 0x0000 |
| 0x2B9B | 0x1155 | 0x0000 | 0x0000 | 0x0000 |
| 0x2B9C | 0x1212 | 0x1213 | 0x1214 | 0x0000 |
| 0x2B9D | 0x0000 | 0x1215 | 0x1216 | 0x1217 |
| 0x2B9E | 0x13B9 | 0x13B9 | 0x13B9 | 0x13B9 |
| 0x2BC0 | 0x10EE | 0x1090 | 0x0000 | 0x0000 |
| 0x2BC1 | 0x0000 | 0x13C5 | 0x13C7 | 0x13C6 |
| 0x2C24 | 0x121A | 0x0000 | 0x0000 | 0x0000 |
| 0x2C31 | 0x0000 | 0x0000 | 0x1161 | 0x1162 |
| 0x2C32 | 0x0000 | 0x0000 | 0x1161 | 0x1162 |
| 0x2C37 | 0x0000 | 0x1163 | 0x0000 | 0x0000 |
| 0x2C38 | 0x0000 | 0x1163 | 0x0000 | 0x0000 |
| 0x2C39 | 0x0000 | 0x0000 | 0x1076 | 0x0000 |
| 0x2C3A | 0x0000 | 0x0000 | 0x1076 | 0x0000 |
| 0x2C3B | 0x1164 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C3C | 0x1164 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C47 | 0x0000 | 0x0000 | 0x1015 | 0x1014 |
| 0x2C48 | 0x0000 | 0x0000 | 0x1015 | 0x1014 |
| 0x2C49 | 0x1165 | 0x1166 | 0x0000 | 0x0000 |
| 0x2C4A | 0x1165 | 0x1166 | 0x0000 | 0x0000 |
| 0x2C4B | 0x1072 | 0x121C | 0x121B | 0x1168 |
| 0x2C4C | 0x1072 | 0x121C | 0x121B | 0x1168 |
| 0x2C4D | 0x116A | 0x116B | 0x0000 | 0x116C |
| 0x2C4E | 0x116A | 0x116B | 0x0000 | 0x116C |
| 0x2C4F | 0x0000 | 0x106E | 0x0000 | 0x0000 |
| 0x2C50 | 0x0000 | 0x106E | 0x0000 | 0x0000 |
| 0x2C51 | 0x0000 | 0x106F | 0x0000 | 0x0000 |
| 0x2C52 | 0x0000 | 0x106F | 0x0000 | 0x0000 |
| 0x2C53 | 0x0000 | 0x121D | 0x0000 | 0x0000 |
| 0x2C54 | 0x0000 | 0x121D | 0x0000 | 0x0000 |
| 0x2C61 | 0x0000 | 0x0000 | 0x0000 | 0x116D |
| 0x2C62 | 0x0000 | 0x0000 | 0x0000 | 0x116D |
| 0x2C6D | 0x116E | 0x1171 | 0x1170 | 0x116F |
| 0x2C6E | 0x116E | 0x1171 | 0x1170 | 0x116F |
| 0x2C71 | 0x1172 | 0x1016 | 0x121E | 0x1014 |
| 0x2C72 | 0x1172 | 0x1016 | 0x121E | 0x1014 |
| 0x2C84 | 0x0000 | 0x13BA | 0x0000 | 0x0000 |
| 0x2C85 | 0x0000 | 0x13BA | 0x0000 | 0x0000 |
| 0x2C9C | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2C9D | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2C9E | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2C9F | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2CA0 | 0x1174 | 0x121F | 0x1175 | 0x1176 |
| 0x2CA1 | 0x1174 | 0x121F | 0x1175 | 0x1176 |
| 0x2CA8 | 0x1178 | 0x0000 | 0x0000 | 0x0000 |
| 0x2CA9 | 0x1178 | 0x0000 | 0x0000 | 0x0000 |
| 0x2CEF | 0x1220 | 0x117B | 0x117C | 0x117A |
| 0x2CF0 | 0x0000 | 0x0000 | 0x1221 | 0x1222 |
| 0x2CF1 | 0x1223 | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF8 | 0x1224 | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF9 | 0x1181 | 0x0000 | 0x1225 | 0x1226 |
| 0x2CFA | 0x1181 | 0x0000 | 0x1225 | 0x1226 |
| 0x2CFF | 0x1227 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D00 | 0x0000 | 0x0000 | 0x1228 | 0x1229 |
| 0x2D01 | 0x0000 | 0x0000 | 0x122A | 0x1186 |
| 0x2D02 | 0x122B | 0x0000 | 0x0000 | 0x0000 |
| 0x2D03 | 0x0000 | 0x0000 | 0x122C | 0x122D |
| 0x2D04 | 0x118A | 0x0000 | 0x0000 | 0x0000 |
| 0x2D05 | 0x122E | 0x0000 | 0x0000 | 0x0000 |
| 0x2D0F | 0x0000 | 0x122F | 0x1231 | 0x1230 |
| 0x2D14 | 0x0000 | 0x0000 | 0x1234 | 0x1235 |
| 0x2D1A | 0x1236 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D1B | 0x118F | 0x0000 | 0x1237 | 0x1238 |
| 0x2D1C | 0x0000 | 0x0000 | 0x1237 | 0x1238 |
| 0x2D28 | 0x0000 | 0x0000 | 0x1192 | 0x1239 |
| 0x2D29 | 0x123A | 0x0000 | 0x1196 | 0x1195 |
| 0x2D32 | 0x0000 | 0x0000 | 0x123C | 0x123B |
| 0x2D6E | 0x1197 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D70 | 0x119B | 0x119E | 0x119C | 0x119D |
| 0x2D71 | 0x123D | 0x11A1 | 0x123F | 0x123E |
| 0x2D72 | 0x0000 | 0x0000 | 0x1240 | 0x11A3 |
| 0x2D75 | 0x1241 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D76 | 0x1242 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D78 | 0x1243 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DBF | 0x1244 | 0x10B5 | 0x1246 | 0x1245 |
| 0x2DCA | 0x11A8 | 0x1274 | 0x11AA | 0x0000 |
| 0x2DCB | 0x1248 | 0x1249 | 0x0000 | 0x0000 |
| 0x2DCF | 0x124A | 0x1274 | 0x11AA | 0x0000 |
| 0x2DD7 | 0x11A8 | 0x1274 | 0x124B | 0x0000 |
| 0x2DD9 | 0x124C | 0x10B5 | 0x124D | 0x0000 |
| 0x2DDA | 0x1275 | 0x1274 | 0x0000 | 0x0000 |
| 0x2DDB | 0x0000 | 0x1247 | 0x0000 | 0x0000 |
| 0x2DDC | 0x11A8 | 0x1247 | 0x11AA | 0x0000 |
| 0x2DDD | 0x124F | 0x10B5 | 0x0000 | 0x0000 |
| 0x2DDE | 0x1250 | 0x1251 | 0x0000 | 0x124F |
| 0x2DDF | 0x1250 | 0x1251 | 0x0000 | 0x124F |
| 0x2DEB | 0x0000 | 0x10BB | 0x1031 | 0x1032 |
| 0x2DEC | 0x1252 | 0x0000 | 0x10BD | 0x0000 |
| 0x2DED | 0x10BE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E24 | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E25 | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E26 | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E27 | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E28 | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E29 | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E2A | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E2B | 0x12EE | 0x0000 | 0x0000 | 0x0000 |
| 0x2E30 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E31 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E32 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E33 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E34 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E35 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E36 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E37 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E68 | 0x1253 | 0x0000 | 0x1254 | 0x11B6 |
| 0x2E69 | 0x1253 | 0x0000 | 0x1254 | 0x11B6 |
| 0x2E6A | 0x1253 | 0x0000 | 0x1254 | 0x11B6 |
| 0x2E6B | 0x1253 | 0x0000 | 0x1254 | 0x1255 |
| 0x2E6E | 0x12ED | 0x0000 | 0x0000 | 0x0000 |
| 0x2E6F | 0x12ED | 0x0000 | 0x0000 | 0x0000 |
| 0x2E72 | 0x1253 | 0x0000 | 0x11B9 | 0x11B8 |
| 0x2E73 | 0x11BA | 0x0000 | 0x0000 | 0x0000 |
| 0x2E7C | 0x10DC | 0x1256 | 0x0000 | 0x0000 |
| 0x2E8B | 0x1257 | 0x1256 | 0x0000 | 0x1258 |
| 0x2E8C | 0x1259 | 0x125A | 0x0000 | 0x11C0 |
| 0x2E8D | 0x125B | 0x10D8 | 0x0000 | 0x125C |
| 0x2E97 | 0x125D | 0x125E | 0x10DC | 0x1055 |
| 0x2EA0 | 0x11BE | 0x1071 | 0x11C1 | 0x11C0 |
| 0x2EB8 | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0x2EBA | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0x2EBB | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0x2EBC | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0x2EBD | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0x2EBE | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0x2ECC | 0x0000 | 0x0000 | 0x0000 | 0x10DA |
| 0x2ECD | 0x0000 | 0x0000 | 0x0000 | 0x1091 |
| 0x2ECE | 0x0000 | 0x0000 | 0x0000 | 0x10E4 |
| 0x2ECF | 0x0000 | 0x0000 | 0x0000 | 0x1055 |
| 0x2ED0 | 0x0000 | 0x0000 | 0x0000 | 0x10E5 |
| 0x2ED1 | 0x0000 | 0x0000 | 0x0000 | 0x10DD |
| 0x2ED2 | 0x0000 | 0x0000 | 0x0000 | 0x10E6 |
| 0x2ED3 | 0x0000 | 0x0000 | 0x0000 | 0x10E7 |
| 0x2EE0 | 0x13BB | 0x10B5 | 0x10EE | 0x1090 |
| 0x2EE1 | 0x13BD | 0x0000 | 0x13BE | 0x13BC |
| 0x2EEA | 0x0000 | 0x0000 | 0x1060 | 0x1015 |
| 0x2EEC | 0x125F | 0x0000 | 0x0000 | 0x1260 |
| 0x2EF4 | 0x11C7 | 0x0000 | 0x0000 | 0x0000 |
| 0x2EF5 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2EFE | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F08 | 0x13CB | 0x0000 | 0x1015 | 0x1014 |
| 0x2F09 | 0x13CC | 0x0000 | 0x0000 | 0x118D |
| 0x2F0B | 0x0000 | 0x0000 | 0x13BF | 0x12EF |
| 0x2F0D | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F10 | 0x0000 | 0x0000 | 0x0000 | 0x1091 |
| 0x2F11 | 0x10F0 | 0x0000 | 0x10DD | 0x10F2 |
| 0x2F12 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F17 | 0x0000 | 0x0000 | 0x0000 | 0x11C8 |
| 0x2F44 | 0x1261 | 0x1263 | 0x1262 | 0x1264 |
| 0x2F45 | 0x11CD | 0x1265 | 0x11CF | 0x0000 |
| 0x2F46 | 0x0000 | 0x1266 | 0x1268 | 0x1267 |
| 0x2F4E | 0x0000 | 0x1269 | 0x11D3 | 0x118D |
| 0x2F4F | 0x11D4 | 0x0000 | 0x11D5 | 0x11D6 |
| 0x2F50 | 0x11D7 | 0x0000 | 0x0000 | 0x126A |
| 0x2F59 | 0x0000 | 0x11D9 | 0x0000 | 0x0000 |
| 0x2F5A | 0x0000 | 0x11DA | 0x0000 | 0x0000 |
| 0x2F62 | 0x11DB | 0x0000 | 0x0000 | 0x0000 |
| 0x2F67 | 0x0000 | 0x126B | 0x0000 | 0x0000 |
| 0x2F6C | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F71 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F77 | 0x126C | 0x126D | 0x118C | 0x118D |
| 0x2F78 | 0x0000 | 0x0000 | 0x1015 | 0x1014 |
| 0x2F7B | 0x126E | 0x0000 | 0x0000 | 0x0000 |
| 0x2F80 | 0x11C2 | 0x10B9 | 0x0000 | 0x0000 |
| 0x2F8A | 0x126F | 0x11E1 | 0x1191 | 0x1190 |
| 0x2F94 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F9E | 0x1018 | 0x1071 | 0x1270 | 0x0000 |
| 0x2FA3 | 0x1271 | 0x0000 | 0x0000 | 0x0000 |
| 0xCD87 | 0x0000 | 0x1272 | 0x11EA | 0x1273 |
| 0xCD8B | 0x0000 | 0x1272 | 0x11EA | 0x1273 |
| 0xCD97 | 0x1275 | 0x1274 | 0x13C9 | 0x13C8 |
| 0xCD9B | 0x1111 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDA1 | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDA2 | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDA3 | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDA7 | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDAA | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDAC | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDB0 | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDB3 | 0x1275 | 0x1274 | 0x13C9 | 0x13C8 |
| 0xCDB7 | 0x0000 | 0x10B9 | 0x0000 | 0x0000 |
| 0xCDEB | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDED | 0x1275 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDEE | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDEF | 0x0000 | 0x1274 | 0x0000 | 0x0000 |
| 0xCDF9 | 0x12F1 | 0x10B9 | 0x0000 | 0x0000 |
| 0xCDFA | 0x12F1 | 0x10B9 | 0x0000 | 0x0000 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 320 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x1014 | Kurzschluss nach Plus |
| 0x1015 | Kurzschluss nach Minus |
| 0x1016 | Leitungsunterbrechung |
| 0x1018 | Signal unplausibel |
| 0x101C | obere Schwelle Pumpenstrom bei Referenzmessung |
| 0x101D | Pumpenstromschwelle bei Ventilprüfung erreicht |
| 0x101E | Abbruch wegen Stromschwankungen bei Feinleckprüfung |
| 0x101F | untere Schwelle Pumpenstrom bei Referenzmessung |
| 0x1028 | Sensorsignale zueinander unplausibel |
| 0x1029 | Lagereglerüberwachung |
| 0x102A | keine Anschläge gelernt |
| 0x102E | Relais-Fehler |
| 0x102F | Kurzschluss der Motorleitungen |
| 0x1031 | Unterspannung |
| 0x1032 | Überspannung |
| 0x1039 | Exzenterwinkel fährt nicht auf Vollhubposition |
| 0x1055 | Übertemperatur |
| 0x1060 | Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x106E | Unterbrechung Abgleichsleitung |
| 0x106F | Unterbrechung Nernstleitung |
| 0x1071 | Kommunikationsfehler |
| 0x1072 | Initialisierungsfehler |
| 0x1076 | Sondensignal zu träge |
| 0x1090 | Signal oberhalb Schwelle |
| 0x1091 | elektrisch |
| 0x10B5 | kein Signal |
| 0x10B9 | Timeout |
| 0x10BB | batterieloser Betrieb |
| 0x10BD | Tiefentladung |
| 0x10BE | Ruhestromverletzung |
| 0x10D8 | Systemfehler |
| 0x10DA | keine Kommunikation über BSD-Schnittstelle |
| 0x10DC | Generatortyp unplausibel |
| 0x10DD | mechanisch |
| 0x10E4 | elektrisch berechnet |
| 0x10E5 | Übertemperatur berechnet |
| 0x10E6 | Reglertyp nicht plausibel |
| 0x10E7 | Generatortyp nicht plausibel |
| 0x10EE | Signal unterhalb Schwelle |
| 0x10F0 | keine Kommunikation |
| 0x10F2 | Hardwaredefekt |
| 0x1111 | Prüfsumme ungleich errechnetem Wert |
| 0x1113 | Verbrennungsaussetzer im Warmlauf, emissionsverschlechternd |
| 0x1114 | Verbrennungsaussetzer betriebswarm, emissionsverschlechternd |
| 0x1115 | Verbrennungsaussetzer mit Zylinderabschaltung |
| 0x1116 | kein Raddrehzahlsignal erhalten |
| 0x1117 | Radgeschwindigkeit zu hoch |
| 0x111D | System zu mager additiv pro Zeit zu groß |
| 0x1120 | Feinleck erkannt |
| 0x1121 | Leckage größer 1,0mm |
| 0x1123 | Tankentlüftungssystem |
| 0x1124 | Tankfüllstandssignal unplausibel |
| 0x1125 | CAN, Ungültigkeitswert empfangen |
| 0x1126 | Magnetloss-Fehler |
| 0x1127 | Reset-Fehler |
| 0x112A | Parity-Fehler oder kein Signal |
| 0x112B | Sensorversorgungsspannung zu klein |
| 0x112C | Sensorversorgungsspannung zu hoch |
| 0x112D | Fehler unteres Lernfenster |
| 0x112E | Verstellbereich fehlerhaft |
| 0x112F | Drehrichtungserkennung |
| 0x1130 | ROM-Test-Fehler |
| 0x1131 | EEPROM-Test-Fehler |
| 0x1132 | Watchdog oder Temperatursensorfehler |
| 0x1133 | RAM-Test-Fehler |
| 0x1134 | Ansteuerungsfehler allgemein |
| 0x1135 | Spannung zu klein |
| 0x1136 | Spannung zu hoch |
| 0x1138 | Drehzahlfüllungsbegrenzung |
| 0x1139 | Anschläge lernen notwendig |
| 0x113C | Temperatur E-Motor zu hoch |
| 0x113D | Steuergerätetemperatur zu hoch |
| 0x113E | maximale Anzahl der Minhubanschläge überschritten |
| 0x1141 | Anschlagadaptionen außerhalb gültigem Bereich |
| 0x1143 | Korrelationsfehler, ein Zahn Versatz |
| 0x1144 | Leitungsunterbrechung, Drehzahlsignal |
| 0x1146 | Zahnkorrektur bei einem Zahn zuwenig |
| 0x1147 | Zahnkorrektur bei einem Zahn zuviel |
| 0x1148 | unplausible Phasenflankenanzahl |
| 0x1149 | Lage der Phasenflanken oder Einbaulage außerhalb Toleranzen |
| 0x1151 | Aktualitätszähler EEPROM und RAMBACKUP unterschiedlich |
| 0x1154 | Rechnerüberwachung: RAM |
| 0x1155 | Rechnerüberwachung: ROM |
| 0x115A | Plausibilitätsfehler |
| 0x115F | CAN Botschaft fehlerhaft |
| 0x1161 | Offsetprüfung, System zu mager |
| 0x1162 | Offsetprüfung, System zu fett |
| 0x1163 | Heizereinkopplung auf Signalpfad |
| 0x1164 | Sonde an Luft |
| 0x1165 | Signal zu mager |
| 0x1166 | Signal zu fett |
| 0x1168 | Signalkreisaptionswert zu hoch |
| 0x116A | Signalspannung im Schub zu klein infolge offener Pumpstromleitung |
| 0x116B | Unterbrechung Pumpstrompfad |
| 0x116C | Lambdaregelwert oberhalb Schwelle infolge offener Pumpstromleitung |
| 0x116D | Nernstzellenwiderstand oder Keramiktemperatur unplausibel, Leitungs- oder Heizerfehler |
| 0x116E | Sonde dynamisch zu langsam |
| 0x116F | Signal überschreitet Schwellwert nicht |
| 0x1170 | Signal unterschreitet Schwellwert nicht |
| 0x1171 | Schubspannungsschwelle nicht erreicht |
| 0x1172 | Heiztakteinkopplung auf Signal |
| 0x1174 | Innenwiderstand der Nernstzelle unplausibel oder zu späte Betriebsbereitschaft |
| 0x1175 | RI-Regler dauerhaft am unteren Anschlag |
| 0x1176 | RI-Regler dauerhaft am oberen Anschlag |
| 0x1178 | Sondenheizung defekt (Innenwiderstand) |
| 0x117A | Kurzschluss |
| 0x117B | Lastabfall |
| 0x117C | Überlastung |
| 0x1181 | unplausibel zu Ersatzwert aus Füllung |
| 0x1186 | Fehler bei Federprüfung 'Öffnen', Abbruch Feder öffnet nicht |
| 0x118A | UMA-Lernen während Urinitialisierung abgebrochen |
| 0x118C | untere Schwelle unterschritten |
| 0x118D | obere Schwelle überschritten |
| 0x118F | Gleichlauffehler zwischen PWG1 und PWG2 |
| 0x1190 | Spannungsschwellwert überschritten |
| 0x1191 | Spannungsschwellwert unterschritten |
| 0x1192 | Signal unterhalb Schwelle, Kurzschluss nach Minus |
| 0x1195 | Drucksensor hat obere Schwelle überschritten |
| 0x1196 | Drucksensor hat untere Schwelle unterschritten |
| 0x1197 | Funktionsüberwachung Momentenvergleich |
| 0x119B | Reaktionsüberwachung |
| 0x119C | Zündwinkelüberwachung |
| 0x119D | RL-Überwachung |
| 0x119E | ADC-Überwachung |
| 0x11A1 | Varianten Codierungsüberwachung |
| 0x11A3 | TPU-Überwachung |
| 0x11A8 | Checksumme fehlerhaft |
| 0x11AA | Alive-Fehler |
| 0x11B1 | Signal nicht plausibel, Zündkreisüberwachung |
| 0x11B2 | Übertemperaturabschaltung oder Signalabfall |
| 0x11B3 | Kurzschluss nach Plus, Nichtimpedanz |
| 0x11B4 | Übergangswiderstand, Hochimpedanz |
| 0x11B6 | Motor mechanisch zu laut oder Sensor außerhalb Toleranz (Empfindlichkeit) |
| 0x11B8 | Testimpulsfehler |
| 0x11B9 | Nulltestfehler |
| 0x11BA | SPI Kommunikation unplausibel |
| 0x11BE | Permittivitätsmessung fehlerhaft |
| 0x11C0 | Temperaturmessung fehlerhaft |
| 0x11C1 | Niveaumessung fehlerhaft |
| 0x11C2 | unplausibel |
| 0x11C6 | Kaltstart, Nebenschluss erkannt |
| 0x11C7 | Thermostat fehlerhaft |
| 0x11C8 | Maximalwert Öltemperatur überschritten |
| 0x11CD | Mehr als 3 Parity-Fehler erkannt |
| 0x11CF | Empfangsfehler des EWS-Telegramms (Start-, Stopbit- oder Framefehler) |
| 0x11D3 | keine Signaländerungen |
| 0x11D4 | Geschwindigkeit unplausibel |
| 0x11D5 | Mindestgeschwindigkeit im Schub nicht erreicht |
| 0x11D6 | Mindestgeschwindigkeit unter Last nicht erreicht |
| 0x11D7 | Geschwindigkeitssignal vom Kombi und ASC nicht kompatibel |
| 0x11D9 | Start in laufenden Motor |
| 0x11DA | Signalfehler Startautomatik |
| 0x11DB | Prüfresultat unplausibel |
| 0x11E1 | Stromversorgung instabil |
| 0x11EA | CAN Baustein DPRAM defekt |
| 0x11EB | Aussetzer aufgrund leerem Tank |
| 0x11EC | Untere Plausibilitätsschwelle unterschritten (obere Multipl.) |
| 0x11ED | Obere Plausibilitätsschwelle überschritten (obere Multipl.) |
| 0x11EE | System zu fett additiv pro Zeit zu klein |
| 0x11EF | Untere Plausibilitätsschwelle unterschritten (Gemisch zu fett) |
| 0x11F0 | Obere Plausibilitätsschwelle überschritten (Gemisch zu mager) |
| 0x11F1 | min Fehler additiv |
| 0x11F2 | max Fehler additiv |
| 0x11F3 | max Fehler multiplikativ |
| 0x11F4 | min Fehler multiplikativ |
| 0x11F5 | Katalysator-Wirkungsgrad unter Schwellwert |
| 0x11F6 | 'Minimalwert' erkannt (Kleinstleck, keine MIL on) |
| 0x11F7 | nicht  korrekt geschlossen |
| 0x11F8 | Kurzschluss nach Masse |
| 0x11F9 | Kurzschluss nach Ubatt |
| 0x11FA | Gradientenüberschreitung / Ident |
| 0x11FB | Datenkonformität |
| 0x11FC | Stack-Test-Fehler |
| 0x11FD | Exzenterwinkel Überlast erkennt Fehler |
| 0x11FE | Strom E-Motoransteuerung zu hoch |
| 0x11FF | Überlastschutz VVT-System |
| 0x1200 | Regelanschlag zu lange, zu groß |
| 0x1201 | Nockenwellenverstellung hat Frühposition nicht erreicht |
| 0x1202 | Nockenwellenverstellung hat Spätposition nicht erreicht |
| 0x1203 | gestörtes Drehzahlsignal |
| 0x1204 | Kurbelwellenzahnfehler oder Lückenverlust |
| 0x1205 | keine Master NW vorhanden |
| 0x1206 | Leitungsunterbrechung oder Überlastung |
| 0x1207 | E_Disamot 'Temperaturgrenzwert Motorschutzmodell' (5 s entprellt) |
| 0x1208 | Reglerüberwachung 'Regeldifferenz zu groß' (0,1 s entprellt) |
| 0x1209 | Potimax 'Potispannung im oberen Diagnosebereich' (30 ms entprellt) |
| 0x120A | Potimin 'Potispannung im unteren Diagnosebereich' (30 ms entprellt) |
| 0x120B | E_Disawarn 'Temperaturschwelle Motorschutzmodell' (5 s entprellt) |
| 0x120C | Pulsation unterhalb Schwelle |
| 0x120D | Pulsation oberhalb Schwelle |
| 0x120E | LL-Steller Öffnung zu gering |
| 0x120F | LL-Steller Öffnung zu groß oder Leckluft |
| 0x1210 | Schreibfehler, RAM Backup Fehler |
| 0x1211 | Lesefehler, RAM Backup Fehler |
| 0x1212 | Rechnerüberwachung RESET |
| 0x1213 | Reset TPU-Überwachung |
| 0x1214 | Reset TPU-RAM |
| 0x1215 | Fehler F/A-Kom. FR-UM aktiv, SG-Fehler |
| 0x1216 | Uberspannung auf VCC geheilt, SG-Fehler |
| 0x1217 | Uberspannung auf VCC aktiv, SG-Fehler |
| 0x1218 | Umgebungstemperatur grösser Modelltemperatur |
| 0x1219 | Umgebungstemperatur kleiner Modelltemperatur |
| 0x121A | Vertauschte Lambdasonden |
| 0x121B | Ubatt low |
| 0x121C | Kommunikation SPI gestört |
| 0x121D | Unterbrechung virtuelle Masse |
| 0x121E | Adernschluß oder CSD (Referenzluft vergiftet) |
| 0x121F | Kalibrierwiderstand im SG fehlerhaft |
| 0x1220 | interner Kommunikationfehler |
| 0x1221 | DK-Lagereg. klemmt kurzzeitig |
| 0x1222 | DK-Lagereg. klemmt anhaltend |
| 0x1223 | DV-E Lageabweichung |
| 0x1224 | Fehler DK-Poti 1 oder DK-Poti 2 |
| 0x1225 | Bereichsverletzung nach unten |
| 0x1226 | Bereichsverletzung nach oben |
| 0x1227 | DV-E Fehler bei Verstärkerabgleich |
| 0x1228 | DV-E Fehler bei Prüfung der öffnenden Feder |
| 0x1229 | DV-E Fehler bei Prüfung der Rückstellfeder |
| 0x122A | Klappe läßt sich nicht von UMA schließen, weil Feder nicht öffnet |
| 0x122B | DV-E Fehler bei Prüfung Notluftposition |
| 0x122C | Lernverbot Status Prüfbedingung = 27 |
| 0x122D | Lernverbot Status Prüfbedingung &gt;0 aber nicht 27 |
| 0x122E | Fehler bei UMA-Lernen (Wiederholung) |
| 0x122F | Kurzschluss oder Leitungsunterbrechung |
| 0x1230 | Wackelkontakt (Periodendauer unplausibel), niedrige Frequenz |
| 0x1231 | Wackelkontakt (Periodendauer unplausibel), hohe Frequenz |
| 0x1232 | Luftmasse gegenüber Modell zu gross |
| 0x1233 | Luftmasse gegenüber Modell zu gering |
| 0x1234 | Kurzschluss, minimale Periodendauer unterschritten |
| 0x1235 | Kurzschluss, maximale Periodendauer überschritten |
| 0x1236 | PWG1 oder PWG2 fehlerhaft oder außerhalb der Toleranz |
| 0x1237 | Spannung unterhalb Min-Wert |
| 0x1238 | Spannung oberhalb Max-Wert |
| 0x1239 | Signal oberhalb Schwelle, Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x123A | Plausibilität Differenzdrucksensor |
| 0x123B | Saugrohrdruck oberhalb Schwelle |
| 0x123C | Saugrohrdruck unterhalb Schwelle |
| 0x123D | DK-Anschlagüberwachung (UMA) Ebene 2 |
| 0x123E | Kraftstoffkorrektur |
| 0x123F | Plausibilisierung relative Kraftstoffmasse / eingespritzte Kraftstoffmasse |
| 0x1240 | ADC-Testspannung außerhalb zulässigem Bereich |
| 0x1241 | Funktionsüberwachung Drehzahlgeber-, Zuleitung- oder SG-Fehler |
| 0x1242 | Fktüberwachung: Pedalwertgeber-, Zuleitung- oder SG-Fehler |
| 0x1243 | Regelbereichsüberwachung fehlerhaft |
| 0x1244 | CACC-Signal unplausibel |
| 0x1245 | keine Reaktion |
| 0x1246 | Alive |
| 0x1247 | Timeouterkennung |
| 0x1248 | CAN-Schnittstelle, Timeout EGS |
| 0x1249 | CAN-Botschaftsüberwachung EGS (elektronische Getriebesteuerung) - Timeout |
| 0x124A | Plausibilitätsfehler MIL Ansteuerung |
| 0x124B | Aliveprüfung |
| 0x124C | Plausfehler der ARS-Botschaft |
| 0x124D | Aktivitätsfehler CAN-ARS-Botschaft |
| 0x124E | Checksumme fehlerhaft/Alive-Fehler |
| 0x124F | Botschaftüberwachung fehlerhaft |
| 0x1250 | VVT-Botschaft nicht empfangen (DME ALL) |
| 0x1251 | VVT-Botschaft (Sollwertbotschaft) nicht empfangen |
| 0x1252 | Powermanagement defekt |
| 0x1253 | Parityfehler |
| 0x1254 | elektrischer Fehler (Wackelkontakt) oder Sensor locker |
| 0x1255 | Motor mechanisch zu laut oder Sensor außerhalb Toelranz (Empfindlichkeit) |
| 0x1256 | Kommunikationsverlust |
| 0x1257 | IBS Softwareversion nicht kompatibel |
| 0x1258 | erweiterte Kommunikation gestört |
| 0x1259 | Strommessung fehlerhaft |
| 0x125A | Spannungsmessung fehlerhaft |
| 0x125B | Kl 15 Wakeupleitung (Pegel unplausibel) |
| 0x125C | KL15 Masseschluss (Pegel Wakeupleitung) |
| 0x125D | Fehler mechanisch |
| 0x125E | Fehler elektrisch |
| 0x125F | Kühleraustrittstemperatur unplausibel |
| 0x1260 | Signalfehler aus Highside-Check erkannt |
| 0x1261 | Falsche EWS-Telegramme empfangen. Die Fangbereichsrechnung ist für mindestens 5 Telegrammauswertungen fehlgeschlagen. |
| 0x1262 | Kein Startwert programmiert |
| 0x1263 | Fehler beim Programmieren oder Rücksetzen des Startwertes. |
| 0x1264 | 1. Startwert im Flash zerstört. 2- aus 3-Auswahl fehlgeschlagen oder 2. Fehlerrückmeldung: Startwertprogrammierroutine |
| 0x1265 | Timeoutfehler: 10 Sekunden nach Kl. 15 EIN noch kein EWS-Telegramm empfangen, evtl. Leitungsunterbrechung oder Kurzschluss nach Minus) |
| 0x1266 | Schreiben auf die Wechselcodeablage im EEPROM fehlerhaft |
| 0x1267 | Lesen der Wechselcodeablage in EEPROM-Spiegel war fehlerhaft |
| 0x1268 | Fehler Ablage (z.B. Powerfail) |
| 0x1269 | CAN Botschaften fehlerhaft |
| 0x126A | Kombi hat ein Ungültigkeitssignal gesendet |
| 0x126B | Signal inaktiv |
| 0x126C | Vergleich aktueller/letzter Fahrzyklus unplausibel |
| 0x126D | Kontinuitätsfehler |
| 0x126E | unplausibler Öldruckschalter |
| 0x126F | ADC-Fehler, HW-Fehler |
| 0x1270 | Ölverlust |
| 0x1271 | DME noch nicht codiert |
| 0x1272 | CAN-Baustein Bus Off oder CAN-Bus defekt |
| 0x1273 | CAN-Baustein im Zustand Passiv |
| 0x1274 | Timeout CAN-Kommunikation |
| 0x1275 | Alive oder Checksummenfehler |
| 0x12D0 | Berechneter Wert ist zu groß |
| 0x12D1 | Wert außerhalb gültigem Bereich |
| 0x12ED | Bankabschaltung |
| 0x12EE | Brenndauerüberwachung, Signal unplausibel |
| 0x12EF | Ansaugluftemperatur oberhalb Motortemperaturschwelle |
| 0x12F0 | Ansaugluftemperatur unterhalb Motortemperaturschwelle |
| 0x12F1 | Alive oder Checksumme fehlerhaft |
| 0x13B6 | Momentendifferenz oberhalb Schwelle |
| 0x13B7 | Überdrehzahlfehler (Leckluft oder Drosselklappenöffnung zu gross) |
| 0x13B8 | Unterdrehzahlfehler (Drosselklappenöffnung zu klein) |
| 0x13B9 | Fertigungs- oder Transportmodus aktiv |
| 0x13BA | Signalfehler im Schubbetrieb |
| 0x13BB | Signalsprünge detektiert |
| 0x13BC | High-Side Check unplausibel |
| 0x13BD | Stuck-Check unplausibel |
| 0x13BE | Low-Side Check unplausibel |
| 0x13BF | Ansauglufttemperatur unterhalb Motortemperaturschwelle |
| 0x13C5 | CAN Botschaft Ungültig |
| 0x13C6 | Wert oberhalb Schwelle |
| 0x13C7 | Wert unterhalb Schwelle |
| 0x13C8 | Verlustmoment zu gross |
| 0x13C9 | AFS/STE disabled oder Lenkmoment ungültig |
| 0x13CB | Wackelkontakt |
| 0x13CC | Bereichsprüfung unplausibel |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 256 rows × 13 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | MEAS |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TE_W | 8312F1224000 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.008 | 0 | 0 | 0 | ms |
| FR_W | 8312F1224000 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| FR2_W | 8312F1224000 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| VFZG | 8312F1224000 | 0 | 0 | 0x00 | 9 | 2 | -- | 1.25 | 0 | 0 | 0 | km/h |
| NMOT_W | 8312F1224000 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.25 | 0 | 0 | 0 | min-1 |
| NSOL | 8312F1224000 | 0 | 0 | 0x00 | 12 | 2 | -- | 10 | 0 | 0 | 0 | min-1 |
| WNWKWE_W | 8312F1224000 | 0 | 0 | 0x00 | 13 | 5 | -- | 0.1 | 0 | 0 | 0 | GradKW |
| WNWKWA_W | 8312F1224000 | 0 | 0 | 0x00 | 15 | 5 | -- | 0.1 | 0 | 0 | 0 | GradKW |
| TANS | 8312F1224000 | 0 | 0 | 0x00 | 17 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| TMOT | 8312F1224000 | 0 | 0 | 0x00 | 18 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| ZWOUT | 8312F1224000 | 0 | 0 | 0x00 | 19 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad |
| WDKBA | 8312F1224000 | 0 | 0 | 0x00 | 20 | 2 | -- | 0.392156 | 0 | 0 | 0 | % DK |
| MSHFM_W | 8312F1224000 | 0 | 0 | 0x00 | 21 | 5 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| MIIST_W | 8312F1224000 | 0 | 0 | 0x00 | 23 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| UB | 8312F1224000 | 0 | 0 | 0x00 | 25 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| UPWG_W | 8312F1224000 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.0048828 | 0 | 0 | 0 | V |
| TKA | 8312F1224000 | 0 | 0 | 0x00 | 28 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| RKRN_W_0 | 8312F1224000 | 0 | 0 | 0x00 | 29 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| RKRN_W_1 | 8312F1224000 | 0 | 0 | 0x00 | 31 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| RKRN_W_2 | 8312F1224000 | 0 | 0 | 0x00 | 33 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| RKRN_W_3 | 8312F1224000 | 0 | 0 | 0x00 | 35 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| RKRN_W_4 | 8312F1224000 | 0 | 0 | 0x00 | 37 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| RKRN_W_5 | 8312F1224000 | 0 | 0 | 0x00 | 39 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| RKRN_W_6 | 8312F1224000 | 0 | 0 | 0x00 | 41 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| RKRN_W_7 | 8312F1224000 | 0 | 0 | 0x00 | 43 | 5 | -- | 0.0006103 | 0 | 0 | 0 | V |
| DFMONITOR | 8312F1224001 | 0 | 0 | 0x00 | 3 | 2 | -- | 0,390625 | 0 | 0 | 0 | % |
| LUTSFI1 | 8312F1224003 | 0 | 0 | 0x00 | 3 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| LUTSFI2 | 8312F1224003 | 0 | 0 | 0x00 | 5 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| LUTSFI3 | 8312F1224003 | 0 | 0 | 0x00 | 7 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| LUTSFI4 | 8312F1224003 | 0 | 0 | 0x00 | 9 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| LUTSFI5 | 8312F1224003 | 0 | 0 | 0x00 | 11 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| LUTSFI6 | 8312F1224003 | 0 | 0 | 0x00 | 13 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| LUTSFI7 | 8312F1224003 | 0 | 0 | 0x00 | 15 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| LUTSFI8 | 8312F1224003 | 0 | 0 | 0x00 | 17 | 7 | -- | 0.0027756 | 0 | 0 | 0 | (1/min/s)^2 |
| UULSUV | 8312F1224003 | 0 | 0 | 0x00 | 20 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UULSUV2 | 8312F1224003 | 0 | 0 | 0x00 | 22 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| MSNDKO | 8312F1224008 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| FKMSDKA | 8312F1224008 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.00006103 | 0 | 0 | 0 | - |
| FKMSDK | 8312F1224008 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.00006103 | 0 | 0 | 0 | - |
| RKAT | 8312F1224004 | 0 | 0 | 0x00 | 3 | 7 | -- | 0.04687 | 0 | 0 | 0 | % |
| RKAT2 | 8312F1224004 | 0 | 0 | 0x00 | 5 | 7 | -- | 0.04687 | 0 | 0 | 0 | % |
| FRA | 8312F1224004 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| FRA2 | 8312F1224004 | 0 | 0 | 0x00 | 9 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| TEDUB | 8312F1224004 | 0 | 0 | 0x00 | 11 | 2 | -- | 0.01 | 0 | 0 | 0 | s |
| TEDUB2 | 8312F1224004 | 0 | 0 | 0x00 | 12 | 2 | -- | 0.01 | 0 | 0 | 0 | s |
| DYNLSU | 8312F1224004 | 0 | 0 | 0x00 | 13 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| DYNLSU2 | 8312F1224004 | 0 | 0 | 0x00 | 15 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| LAMSONI | 8312F1224004 | 0 | 0 | 0x00 | 17 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| LAMSONI2 | 8312F1224004 | 0 | 0 | 0x00 | 19 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| TATEIST | 8312F1224005 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| VSASPRI | 8312F1224005 | 0 | 0 | 0x00 | 4 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSASPRI2 | 8312F1224005 | 0 | 0 | 0x00 | 6 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSESPRI | 8312F1224005 | 0 | 0 | 0x00 | 8 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSESPRI2 | 8312F1224005 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSATV | 8312F1224005 | 0 | 0 | 0x00 | 12 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| VSATV2 | 8312F1224005 | 0 | 0 | 0x00 | 14 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| VSETV | 8312F1224005 | 0 | 0 | 0x00 | 16 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| VSETV2 | 8312F1224005 | 0 | 0 | 0x00 | 18 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| TAML | 8312F1224005 | 0 | 0 | 0x00 | 20 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| VSAADP | 8312F1224006 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSAADP2 | 8312F1224006 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSEADP | 8312F1224006 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSEADP2 | 8312F1224006 | 0 | 0 | 0x00 | 9 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSAADPFL0 | 8312F1224006 | 0 | 0 | 0x00 | 11 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADPFL1 | 8312F1224006 | 0 | 0 | 0x00 | 12 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADPFL2 | 8312F1224006 | 0 | 0 | 0x00 | 13 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADPFL3 | 8312F1224006 | 0 | 0 | 0x00 | 14 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL0 | 8312F1224006 | 0 | 0 | 0x00 | 15 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL1 | 8312F1224006 | 0 | 0 | 0x00 | 16 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL2 | 8312F1224006 | 0 | 0 | 0x00 | 17 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL3 | 8312F1224006 | 0 | 0 | 0x00 | 18 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL0 | 8312F1224006 | 0 | 0 | 0x00 | 19 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL1 | 8312F1224006 | 0 | 0 | 0x00 | 20 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL2 | 8312F1224006 | 0 | 0 | 0x00 | 21 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL3 | 8312F1224006 | 0 | 0 | 0x00 | 22 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL0 | 8312F1224006 | 0 | 0 | 0x00 | 23 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL1 | 8312F1224006 | 0 | 0 | 0x00 | 24 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL2 | 8312F1224006 | 0 | 0 | 0x00 | 25 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL3 | 8312F1224006 | 0 | 0 | 0x00 | 26 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| KVA_KORR | 8212F121C1 | 0 | 0 | 0x00 | 2 | 3 | -- | 0.001 | 0 | 0 | 0 | % |
| DNLLMV | 8312F130A101 | 0 | 0 | 0x00 | 6 | 3 | -- | 10 | 0 | 0 | 0 | 1/min |
| DNSACMV | 8312F130A101 | 0 | 0 | 0x00 | 7 | 3 | -- | 10 | 0 | 0 | 0 | 1/min |
| DNSLBV | 8312F130A101 | 0 | 0 | 0x00 | 8 | 3 | -- | 10 | 0 | 0 | 0 | 1/min |
| DNFSACMV | 8312F130A101 | 0 | 0 | 0x00 | 9 | 3 | -- | 10 | 0 | 0 | 0 | 1/min |
| DNFSMV | 8312F130A101 | 0 | 0 | 0x00 | 10 | 3 | -- | 10 | 0 | 0 | 0 | 1/min |
| VVTSW | 8312F122400B | 0 | 0 | 0x00 | 3 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTIW | 8312F122400B | 0 | 0 | 0x00 | 5 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTTV | 8312F122400B | 0 | 0 | 0x00 | 7 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| VVTES | 8312F122400B | 0 | 0 | 0x00 | 8 | 2 | -- | 0.5 | -63.5 | 0 | 0 |  |
| VVTSW2 | 8312F122400B | 0 | 0 | 0x00 | 9 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTIW2 | 8312F122400B | 0 | 0 | 0x00 | 11 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTTV2 | 8312F122400B | 0 | 0 | 0x00 | 13 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| VVTES2 | 8312F122400B | 0 | 0 | 0x00 | 14 | 2 | -- | 0.5 | -63.5 | 0 | 0 | - |
| MINHUBVSI | 8312F122400B | 0 | 0 | 0x00 | 17 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| DELTAGVFI | 8312F122400B | 0 | 0 | 0x00 | 19 | 7 | -- | 0.0019532 | 0 | 0 | 0 | - |
| FLUB1 | 8312F122400B | 0 | 0 | 0x00 | 21 | 7 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| FLUB2 | 8312F122400B | 0 | 0 | 0x00 | 23 | 7 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| MINHUBROH | 8312F122400B | 0 | 0 | 0x00 | 27 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| TSG | 8312F122400C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| DMVAD | 8312F122400C | 0 | 0 | 0x00 | 5 | 7 | -- | 0.00305175 | 0 | 0 | 0 | % |
| DPS | 8312F122400C | 0 | 0 | 0x00 | 7 | 7 | -- | 0.0390625 | 0 | 0 | 0 | hPa |
| DPSRAUS | 8312F122400C | 0 | 0 | 0x00 | 9 | 5 | -- | 0.0390625 | -1280 | 0 | 0 | hPa |
| FKMSVVT | 8312F122400C | 0 | 0 | 0x00 | 11 | 5 | -- | 0.00006104 | 0 | 0 | 0 | - |
| FPRSTEP | 8312F122400C | 0 | 0 | 0x00 | 13 | 2 | -- | 1 | 0 | 0 | 0 | - |
| LRNSTEP | 8312F122400C | 0 | 0 | 0x00 | 14 | 2 | -- | 1 | 0 | 0 | 0 | - |
| MSNVVTO | 8312F122400C | 0 | 0 | 0x00 | 15 | 7 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| NNW10 | 8312F122400C | 0 | 0 | 0x00 | 17 | 7 | -- | 0.0009765625 | 0 | 0 | 0 | - |
| NNW11 | 8312F122400C | 0 | 0 | 0x00 | 19 | 7 | -- | 0.0009765625 | 0 | 0 | 0 | - |
| NNW12 | 8312F122400C | 0 | 0 | 0x00 | 21 | 7 | -- | 0.0009765625 | 0 | 0 | 0 | - |
| NNW20 | 8312F122400C | 0 | 0 | 0x00 | 23 | 7 | -- | 0.0009765625 | 0 | 0 | 0 | - |
| NNW21 | 8312F122400C | 0 | 0 | 0x00 | 25 | 7 | -- | 0.0009765625 | 0 | 0 | 0 | - |
| NNW22 | 8312F122400C | 0 | 0 | 0x00 | 27 | 7 | -- | 0.0009765625 | 0 | 0 | 0 | - |
| NSOLFASTA | 8312F122400D | 0 | 0 | 0x00 | 3 | 5 | -- | 0.25 | 0 | 0 | 0 | min-1 |
| RL | 8312F122400D | 0 | 0 | 0x00 | 5 | 5 | -- | 0.0234375 | 0 | 0 | 0 | % |
| RLSOL | 8312F122400D | 0 | 0 | 0x00 | 7 | 5 | -- | 0.0234375 | 0 | 0 | 0 | % |
| TE | 8312F122400D | 0 | 0 | 0x00 | 9 | 5 | -- | 0.008 | 0 | 0 | 0 | ms |
| TE2 | 8312F122400D | 0 | 0 | 0x00 | 11 | 5 | -- | 0.008 | 0 | 0 | 0 | ms |
| VVTSTATUS | 8312F122400D | 0 | 0 | 0x00 | 13 | 5 | -- | 1 | 0 | 0 | 0 | - |
| WDKBAFASTA | 8312F122400D | 0 | 0 | 0x00 | 15 | 5 | -- | 0.0244140625 | 0 | 0 | 0 | %DK |
| WDKS | 8312F122400D | 0 | 0 | 0x00 | 17 | 5 | -- | 0.00152588 | 0 | 0 | 0 | % |
| WPED | 8312F122400D | 0 | 0 | 0x00 | 19 | 5 | -- | 0.0015259 | 0 | 0 | 0 | %PED |
| ZWIST | 8312F122400D | 0 | 0 | 0x00 | 21 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad KW |
| DMLLRI | 8312F122400D | 0 | 0 | 0x00 | 23 | 7 | -- | 0.0030518 | 0 | 0 | 0 | % |
| MIMIN | 8312F122400D | 0 | 0 | 0x00 | 25 | 5 | -- | 0.00152588 | 0 | 0 | 0 | % |
| MDGEN | 8312F122400E | 0 | 0 | 0x00 | 3 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| MDKO | 8312F122400E | 0 | 0 | 0x00 | 4 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| DMRLLR | 8312F122400E | 0 | 0 | 0x00 | 5 | 5 | -- | 0.097647 | 0 | 0 | 0 | % |
| MDWAN | 8312F122400E | 0 | 0 | 0x00 | 8 | 5 | -- | 0.0030518 | 0 | 0 | 0 | % |
| DWKR | 8312F122400E | 0 | 0 | 0x00 | 10 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad KW |
| DZWS | 8312F122400E | 0 | 0 | 0x00 | 11 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad KW |
| DFFGEN | 8312F122400E | 0 | 0 | 0x00 | 12 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| TUMG | 8312F122400E | 0 | 0 | 0x00 | 13 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| DMVADFS | 8312F122400E | 0 | 0 | 0x00 | 14 | 7 | -- | 0.0030518 | 0 | 0 | 0 | % |
| DMVADKO | 8312F122400E | 0 | 0 | 0x00 | 16 | 7 | -- | 0.0030518 | 0 | 0 | 0 | % |
| DLAHI | 8312F122400E | 0 | 0 | 0x00 | 18 | 7 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| DLAHI2 | 8312F122400E | 0 | 0 | 0x00 | 20 | 7 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| RINH | 8312F122400E | 0 | 0 | 0x00 | 22 | 5 | -- | 2 | 0 | 0 | 0 | Ohm |
| RINH2 | 8312F122400E | 0 | 0 | 0x00 | 24 | 5 | -- | 2 | 0 | 0 | 0 | Ohm |
| RKATS | 8312F122400E | 0 | 0 | 0x00 | 26 | 7 | -- | 0.0468749 | 0 | 0 | 0 | % |
| DPSSOL | 8312F122400E | 0 | 0 | 0x00 | 28 | 7 | -- | 0.0390625 | 0 | 0 | 0 | hPa |
| CO_POT | 8312F122400F | 0 | 0 | 0x00 | 5 | 7 | -- | 1 | 0 | 0 | 0 | - |
| UPWG | 8312F122400F | 0 | 0 | 0x00 | 7 | 5 | -- | 0.0048828 | 0 | 0 | 0 | V |
| MINHUB | 8312F122400F | 0 | 0 | 0x00 | 9 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| GVIST | 8312F122400F | 0 | 0 | 0x00 | 12 | 7 | -- | 0.001953125 | 0 | 0 | 0 | - |
| FTBR | 8312F122400F | 0 | 0 | 0x00 | 14 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| FHO | 8312F122400F | 0 | 0 | 0x00 | 16 | 5 | -- | 0.00006104 | 0 | 0 | 0 | - |
| FTVDK | 8312F122400F | 0 | 0 | 0x00 | 18 | 2 | -- | 0.0078125 | 0 | 0 | 0 | - |
| MSNVVTOLL | 8312F122400F | 0 | 0 | 0x00 | 20 | 7 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| VSESPRS | 8312F122400F | 0 | 0 | 0x00 | 24 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| VSE2SPRS | 8312F122400F | 0 | 0 | 0x00 | 26 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| VSASPRS | 8312F122400F | 0 | 0 | 0x00 | 29 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| VSA2SPRS | 8312F122400F | 0 | 0 | 0x00 | 30 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| EVHUBI | 8312F1224010 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| EVHUBI2 | 8312F1224010 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| EVHUBS | 8312F1224010 | 0 | 0 | 0x00 | 9 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| OFWNKADBG | 8312F1224010 | 0 | 0 | 0x00 | 11 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| DFSERESZ | 8312F1224010 | 0 | 0 | 0x00 | 16 | 5 | -- | 1 | 0 | 0 | 0 | - |
| DMVADFK | 8312F1224010 | 0 | 0 | 0x00 | 18 | 7 | -- | 0.0030517 | 0 | 0 | 0 | % |
| DMVADLL | 8312F1224010 | 0 | 0 | 0x00 | 20 | 7 | -- | 0.0030517 | 0 | 0 | 0 | % |
| EXWINKI | 8312F1224010 | 0 | 0 | 0x00 | 22 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| EXWINKI2 | 8312F1224010 | 0 | 0 | 0x00 | 24 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| EXWINKS | 8312F1224010 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| FKMSVVTA | 8312F1224011 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00006104 | 0 | 0 | 0 | - |
| FOFRESZ | 8312F1224011 | 0 | 0 | 0x00 | 5 | 5 | -- | 1 | 0 | 0 | 0 | - |
| MSDIF | 8312F1224011 | 0 | 0 | 0x00 | 7 | 7 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| TABGM | 8312F1224011 | 0 | 0 | 0x00 | 9 | 2 | -- | 5 | -50 | 0 | 0 | Grad C |
| TNSE | 8312F1224011 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.1 | 0 | 0 | 0 | s |
| OZRWPERM | 8312F1224011 | 0 | 0 | 0x00 | 12 | 7 | -- | 10 | 0 | 0 | 0 | - |
| OZRWKVB | 8312F1224011 | 0 | 0 | 0x00 | 14 | 7 | -- | 10 | 0 | 0 | 0 | - |
| OZPERMLOW | 8312F1224011 | 0 | 0 | 0x00 | 24 | 5 | -- | 0.00009155 | 0 | 0 | 0 | - |
| OZPERMEX | 8312F1224011 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.00009155 | 0 | 0 | 0 | - |
| OZPERMOFF | 8312F1224011 | 0 | 0 | 0x00 | 28 | 7 | -- | 0.0001831 | 0 | 0 | 0 | - |
| OZKVBOG | 8312F1224011 | 0 | 0 | 0x00 | 30 | 7 | -- | 0.01831082 | 0 | 0 | 0 | - |
| OZPERMBOG | 8312F1224011 | 0 | 0 | 0x00 | 32 | 7 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| OZOELKM | 8312F1224011 | 0 | 0 | 0x00 | 34 | 7 | -- | 10 | 0 | 0 | 0 | km |
| NADMTLL | 8312F1224012 | 0 | 0 | 0x00 | 3 | 5 | -- | 1 | 0 | 0 | 0 | - |
| NTGLM | 8312F1224012 | 0 | 0 | 0x00 | 5 | 5 | -- | 1 | 0 | 0 | 0 | - |
| NTKLM | 8312F1224012 | 0 | 0 | 0x00 | 7 | 5 | -- | 1 | 0 | 0 | 0 | - |
| NDIPFRO | 8312F1224012 | 0 | 0 | 0x00 | 9 | 5 | -- | 1 | 0 | 0 | 0 | - |
| NKFL | 8312F1224012 | 0 | 0 | 0x00 | 11 | 2 | -- | 1 | 0 | 0 | 0 | - |
| SSLLCNT | 8312F1224012 | 0 | 0 | 0x00 | 12 | 2 | -- | 1 | 0 | 0 | 0 | - |
| MINHUBFAK | 8312F1224012 | 0 | 0 | 0x00 | 15 | 2 | -- | 0.00784314 | 0 | 0 | 0 | - |
| MINADRDY | 8312F1224012 | 0 | 0 | 0x00 | 16 | 2 | -- | 1 | 0 | 0 | 0 | - |
| FDLUBBGL | 8312F1224012 | 0 | 0 | 0x00 | 21 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| OFWNKBG1 | 8312F1224012 | 0 | 0 | 0x00 | 24 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| OFWNKBG2 | 8312F1224012 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| OFWNKMX | 8312F1224012 | 0 | 0 | 0x00 | 28 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| WTSG | 8312F1304101 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| USHK2 | 8312F1304501 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UPWG1 | 8312F1304601 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UPWG2 | 8312F1304701 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| USHK | 8312F1304801 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| WUB | 8312F1304A01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| UDKP2 | 8312F1304C01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.001221 | 0 | 0 | 0 | V |
| UDKP1V | 8312F1304D01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UDKP1 | 8312F1304E01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.001221 | 0 | 0 | 0 | V |
| TPMSHFM | 8312F1304F01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.0001 | 0 | 0 | 0 | V |
| WTMOT | 8312F1305001 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.00488 | 0 | 0 | 0 | V |
| WTFA1 | 8312F1305101 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.00488 | 0 | 0 | 0 | V |
| WTKA | 8312F1305201 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSV | 8312F1305C01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSV2 | 8312F1305D01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSH | 8312F1305E01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSH2 | 8312F1305F01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| DISA | 8312F1306D01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UDDSS | 8312F1306F01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UDSU | 8312F1307001 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UUPTES | 8312F1307401 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| MINHUB_W | 8312F130A301 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| OFWTSTBER | 8312F130A401 | 0 | 0 | 0x00 | 3 | 2 | -- | 1 | 0 | 0 | 0 | - |
| OFWNKTEST | 8312F130A401 | 0 | 0 | 0x00 | 4 | 7 | -- | 0.1 | 0 | 0 | 0 | Grad |
| OSCDKTF | 8212F1211C | 0 | 0 | 0x00 | 4 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| OSCDKTF2 | 8212F1211C | 0 | 0 | 0x00 | 6 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| UBATT | 8312F122402B | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00025 | 6 | 0 | 0 | V |
| IBATT | 8312F122402B | 0 | 0 | 0x00 | 3 | 5 | -- | 0.08 | -200 | 0 | 0 | A |
| TBATT | 8312F122402B | 0 | 0 | 0x00 | 3 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| GENMANUFAK | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 1 | 0 | 0 | 0 | - |
| GENTYPKENN | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 1 | 0 | 0 | 0 | - |
| BSDGENREGV | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 1 | 0 | 0 | 0 | - |
| DFFGEN1 | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| UGEN | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.1 | 10.6 | 0 | 0 | V |
| UFGEN | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.1 | 10.6 | 0 | 0 | V |
| TLRGEN | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.1 | 0 | 0 | 0 | s |
| TLRFGEN | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.1 | 0 | 0 | 0 | s |
| MDGENVF | 8312F122402C | 0 | 0 | 0x00 | 3 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| STIGEN | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 1 | 0 | 0 | 0 | A |
| IERR | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.125 | 0 | 0 | 0 | A |
| IERRGRENZ | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.125 | 0 | 0 | 0 | A |
| IERRFGRENZ | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.125 | 0 | 0 | 0 | A |
| TCHIP | 8312F122402C | 0 | 0 | 0x00 | 3 | 2 | -- | 1 | -40 | 0 | 0 | Grad C |
| FAKIHA | 8312F1224025 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.01 | 0 | 0 | 0 | - |
| OZNIVKRZT | 8312F1224000 | 0 | 0 | 0x00 | 45 | 2 | -- | 0.29296875 | 0 | 0 | 0 | mm |
| OZNIVLANGT | 8312F1224000 | 0 | 0 | 0x00 | 46 | 2 | -- | 0.29296875 | 0 | 0 | 0 | mm |
| OZNIV | 8312F1300E01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.29296875 | 0 | 0 | 0 | mm |
| OZTEMP | 8312F1300E01 | 0 | 0 | 0x00 | 4 | 7 | -- | 0.1 | 0 | 0 | 0 | Grad C |
| OZPERM | 8312F1300E01 | 0 | 0 | 0x00 | 6 | 5 | -- | 0.000091553 | 0 | 0 | 0 | - |
| EISYDKFKAF | 8312F1224008 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.007813 | 0 | 0 | 0 | - |
| EISYDKKOFF | 8312F1224008 | 0 | 0 | 0x00 | 4 | 3 | -- | 8 | 0 | 0 | 0 | kg/h |
| EISYEVFKAF | 8312F1224008 | 0 | 0 | 0x00 | 5 | 2 | -- | 0.007813 | 0 | 0 | 0 | - |
| EISYEVKOFF | 8312F1224008 | 0 | 0 | 0x00 | 6 | 3 | -- | 8 | 0 | 0 | 0 | kg/h |
| AMO_05 | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| AMO_10 | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| AMO_15 | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| AMO_20 | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.000244140625 | 0 | 0 | 0 | - |
| EXWINKKOR | 8312F122402D | 0 | 0 | 0x00 | 0 | 7 | -- | 0.021972656 | 0 | 0 | 0 | Grad |
| MNHUB | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| F_MNHUB | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.00001525879 | 0 | 0 | 0 | - |
| MNHUB_ROH | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| MNHUBVS | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| MNHUBVS_IST | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| MNHUBVSNV | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| F_TIKORRVR | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | mm |
| LURABS_F | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.1 | 0 | 0 | 0 | mm |
| LURDIF_F | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.1 | 0 | 0 | 0 | mm |
| ZW_OFFKORRVR | 8312F122402D | 0 | 0 | 0x00 | 0 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| ENDE |  |  |  |  | 1 | 1 | -- | 1 | 0 | 0 | 0 | - |

<a id="table-bits"></a>
### BITS

Dimensions: 124 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| B_FOFR1 | 19 | 0x01 | 0x01 |
| B_HUBEINGR_INAKT | 3 | 0x08 | 0x08 |
| B_MINHUBEINGR_INAKT | 3 | 0x04 | 0x04 |
| B_ZWEINGR_INAKT | 3 | 0x02 | 0x02 |
| B_GEMISCHEINGR_INAKT | 3 | 0x01 | 0x01 |
| B_KRDWS | 4 | 0x01 | 0x01 |
| B_MIL | 22 | 0x01 | 0x01 |
| B_FS | 7 | 0x01 | 0x01 |
| B_ECULOCKF | 3 | 0x01 | 0x01 |
| B_LRNRDYFAST | 4 | 0x01 | 0x01 |
| B_LLTD | 11 | 0x01 | 0x01 |
| B_LLK | 19 | 0x01 | 0x01 |
| B_TEAKT | 22 | 0x01 | 0x01 |
| B_VVTNOTL | 23 | 0x01 | 0x01 |
| B_NVRBUPOK | 32 | 0x01 | 0x01 |
| B_ATMTPA | 3 | 0x01 | 0x01 |
| B_ATMTPK | 4 | 0x01 | 0x01 |
| B_KH | 13 | 0x01 | 0x01 |
| B_NSUB | 14 | 0x01 | 0x01 |
| B_TE | 15 | 0x01 | 0x01 |
| B_FE | 28 | 0x01 | 0x01 |
| B_SSLL | 13 | 0x01 | 0x01 |
| B_TDAON | 14 | 0x01 | 0x01 |
| B_BGLRDY | 23 | 0x01 | 0x01 |
| B_KL15 | 3 | 0x01 | 0x01 |
| B_ESTART | 3 | 0x02 | 0x02 |
| B_KUPPL | 3 | 0x04 | 0x04 |
| B_BL | 3 | 0x08 | 0x08 |
| B_BR | 3 | 0x10 | 0x10 |
| B_KO | 3 | 0x80 | 0x80 |
| B_LL | 3 | 0x01 | 0x01 |
| B_VL | 3 | 0x02 | 0x02 |
| B_SBBHK2 | 3 | 0x04 | 0x04 |
| B_SBBHK | 3 | 0x08 | 0x08 |
| B_SBBVK2 | 3 | 0x10 | 0x10 |
| B_SBBVK | 3 | 0x20 | 0x20 |
| B_LR2 | 3 | 0x40 | 0x40 |
| B_LR | 3 | 0x80 | 0x80 |
| B_PEDSPORT | 4 | 0X02 | 0X02 |
| B_KD | 4 | 0x04 | 0x04 |
| B_PN | 4 | 0x08 | 0x08 |
| B_ECULOCK | 4 | 0x10 | 0x10 |
| B_TEHB | 4 | 0x20 | 0x20 |
| B_SA | 4 | 0x40 | 0x40 |
| B_LRNRDY | 4 | 0x80 | 0x80 |
| B_KOE | 21 | 0x08 | 0x08 |
| B_HSVE2 | 21 | 0x10 | 0x10 |
| B_HSVE | 21 | 0x20 | 0x20 |
| B_HSHE2 | 21 | 0x40 | 0x40 |
| B_HSHE | 21 | 0x80 | 0x80 |
| B_AKR | 22 | 0x08 | 0x08 |
| B_EBL | 22 | 0x10 | 0x10 |
| B_EKP | 22 | 0x20 | 0x20 |
| B_ETR | 22 | 0x40 | 0x40 |
| B_STA | 22 | 0x80 | 0x80 |
| B_NOKATFZ | 3 | 0x01 | 0x01 |
| B_AUTGET | 3 | 0x02 | 0x02 |
| B_ACC | 3 | 0x04 | 0x04 |
| B_ASCPKW | 3 | 0x08 | 0x08 |
| B_ARSVAR | 3 | 0x10 | 0x10 |
| B_TXUGET | 3 | 0x20 | 0x20 |
| B_KOGER | 3 | 0x40 | 0x40 |
| B_AGR | 3 | 0x80 | 0x80 |
| B_MFL | 4 | 0x01 | 0x01 |
| B_AKRFZ | 4 | 0x02 | 0x02 |
| B_DISA_GESCH_GL_VAR_NEU | 3 | 0x01 | 0x01 |
| B_DISA_GEREG_LAGEM_VAR_NEU | 3 | 0x04 | 0x04 |
| B_ANSKL_GL_VAR_NEU | 3 | 0x08 | 0x08 |
| B_AGR_VAR_NEU | 3 | 0x80 | 0x80 |
| B_ABGK_MONO_GL_VAR_NEU | 4 | 0x01 | 0x01 |
| B_ABGK_Y_GL_VAR_NEU | 4 | 0x02 | 0x02 |
| B_ABGK_STER_GL_VAR_NEU | 4 | 0x04 | 0x04 |
| B_NOKATFZ_VAR_NEU | 4 | 0x08 | 0x08 |
| B_LIN_LSVK_GL_VAR_NEU | 4 | 0x10 | 0x10 |
| B_ZWP_LSVK_GL_VAR_NEU | 4 | 0x20 | 0x20 |
| B_AKRFZ_VAR_NEU | 5 | 0x01 | 0x01 |
| B_SOUNDKL_VAR_NEU | 5 | 0x02 | 0x02 |
| B_GLFVAR_VAR_NEU | 5 | 0x04 | 0x04 |
| B_ELUE400_GL_VAR_NEU | 5 | 0x08 | 0x08 |
| B_ELUE600_GL_VAR_NEU | 5 | 0x10 | 0x10 |
| B_EBLVAR_VAR_NEU | 5 | 0x20 | 0x20 |
| B_MFL_VAR_NEU | 5 | 0x40 | 0x40 |
| B_SPTVAR_VAR_NEU | 5 | 0x80 | 0x80 |
| B_STRVAR_VAR_NEU | 6 | 0x01 | 0x01 |
| B_TOENSVAR_VAR_NEU | 6 | 0x02 | 0x02 |
| B_AKKS_VAR | 6 | 0x04 | 0x04 |
| B_PKKS_VAR | 6 | 0x08 | 0x08 |
| B_HS_GL_VAR_NEU | 6 | 0x10 | 0x10 |
| B_SSG_GL_VAR_NEU | 6 | 0x20 | 0x20 |
| B_EGS_GL_VAR_NEU | 6 | 0x40 | 0x40 |
| B_TXUGET_VAR_NEU | 6 | 0x80 | 0x80 |
| B_ASCPKW_VAR_NEU | 7 | 0x01 | 0x01 |
| B_ACC_VAR_NEU | 7 | 0x02 | 0x02 |
| B_ARSVAR_VAR_NEU | 7 | 0x08 | 0x08 |
| B_AFSVAR_VAR_NEU | 7 | 0x40 | 0x40 |
| B_KOVAR_VAR_NEU | 7 | 0x80 | 0x80 |
| B_IBSDETEC_VAR_NEU | 8 | 0x80 | 0x80 |
| B_KATFZ | 2 | 0x01 | 0x01 |
| B_CDTES | 2 | 0x04 | 0x04 |
| B_CDSLS | 2 | 0x08 | 0x08 |
| B_CDLSV | 2 | 0x20 | 0x20 |
| B_CDHSV | 2 | 0x40 | 0x40 |
| B_CDAGR | 2 | 0x80 | 0x80 |
| B_KATRDY | 3 | 0x01 | 0x01 |
| B_TESRDY | 3 | 0x04 | 0x04 |
| B_SLSRDY | 3 | 0x08 | 0x08 |
| B_LSRDY | 3 | 0x20 | 0x20 |
| B_HSRDY | 3 | 0x40 | 0x40 |
| B_AGRRDY | 3 | 0x80 | 0x80 |
| B_FGRAT | 2 | 0x01 | 0x01 |
| B_FGRHSA | 2 | 0x02 | 0x02 |
| B_FGRTBE | 2 | 0x04 | 0x04 |
| B_FGRTSE | 2 | 0x08 | 0x08 |
| B_FGRTVE | 2 | 0x10 | 0x10 |
| B_FGRTWA | 2 | 0x20 | 0x20 |
| L_FGR | 2 | 0x40 | 0x40 |
| B_ACC_FGR | 2 | 0x80 | 0x80 |
| B_GAD | 2 | 0x01 | 0x01 |
| Z_LSH | 2 | 0x02 | 0x02 |
| Z_LSH2 | 2 | 0x02 | 0x02 |
| B_NMOT | 15 | 0x01 | 0x01 |
| B_MINHUBVS | 16 | 0x01 | 0x01 |
| B_FBGL | 25 | 0x01 | 0x01 |
| B_BGL | 26 | 0x01 | 0x01 |

<a id="table-vvtstatusbg2-2"></a>
### VVTSTATUSBG2_2

Dimensions: 8 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Anschlaege werden gerade gelernt |
| 0x01 | Lernanforderung durch VVT-SG zurueckgewiesen |
| 0x02 | Lernen durch DME abgebrochen |
| 0x03 | Lernen durch VVT abgebrochen |
| 0x05 | Keine Anforderung zum Anschlaglernen |
| 0x06 | Lernvorgang beendet |
| 0x07 | Signal ungueltig |
| 0xXY | Fehlerhafter Status |

<a id="table-ewsstart"></a>
### EWSSTART

Dimensions: 5 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | ME9.2 bereit, Startwert zu empfangen |
| 0x01 | kein freier Startwert mit Freigabe vorhanden |
| 0x02 | noch kein Startwert gespeichert |
| 0x03 | Startwert nicht plausibel (wie im DS2-LH definiert) |
| 0xXY | Fehlerhafter Status |

<a id="table-ewsempfangsstatus"></a>
### EWSEMPFANGSSTATUS

Dimensions: 15 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Startwertprogrammierung bzw. -ruecksetzen war erfolgreich |
| 0x01 | falscher Startwert beim Ruecksetzen (EWS u. DME passen ni. zusammen)  |
| 0x02 | Telegramminhalt war kein Startwert (event. Wechselcode) |
| 0x03 | Schnittstellenfehler DWA: Frame o. Parity oder kein Signal (Timeout) |
| 0x04 | Prozess laeuft |
| 0x05 | Programmierung bzw. Ruecksetzen im Fahrzyklus noch nicht ausgefuehrt |
| 0x06 | gleiche Zufallszahl wie bei vorherigem Ruecksetzen trotz Weiterschaltung |
| 0x07 | noch kein Startwert programmiert |
| 0x10 | Startwert nicht korrekt in Flash programmiert |
| 0x11 | Wechselcode nicht korrekt in EEPROM-Spiegel programmiert |
| 0x12 | Zufallszahl nicht korrekt in EEPROM-Spiegel programmiert |
| 0x20 | Fehler bei Startwertprogrammierroutine |
| 0x21 | 2-aus-3-Startwertablage im Flash nicht in Ordnung |
| 0x22 | Ablage im EEPROM-Spiegel nicht in Ordnung |
| 0xXY | Fehlerhafter Status |

<a id="table-regel"></a>
### REGEL

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | --                                                     |
| 0x01 | Regelung AUS, Einschaltbedingung noch nicht erfuellt |
| 0x02 | Regelung EIN |
| 0x04 | Regelung AUS wegen Fahrbedingung |
| 0x08 | Regelung AUS wegen erkanntem Fehler |
| 0x10 | Regelung EIN mit Einschraenkung |
| 0xXY | ?? |

<a id="table-tevstatus"></a>
### TEVSTATUS

Dimensions: 9 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Systemtest TEV laeuft |
| 0x01 | Systemtest kann nicht gestartet werden |
| 0x05 | Systemtest ist nicht gestartet |
| 0x06 | Systemtest TEV ist beendet |
| 0x08 | TEV noch nicht geschlossen für Drehzahlpruefung |
| 0x09 | Beladungspruefung laeuft |
| 0x0A | Systemtest TEV beendet ohne Fehler |
| 0x0B | Systemtest TEV beendet mit Fehler |
| 0xXY | Status Systemtest TEV kann nicht ausgegeben werden |

<a id="table-stagedmtl"></a>
### STAGEDMTL

Dimensions: 19 rows × 2 columns

| STAGE | TEXT |
| --- | --- |
| 0x00 | Funktion laeuft |
| 0x01 | Referenzleckmessung laeuft |
| 0x02 | Grobleckpruefung/verlaengerte Grobleckpruefung laeuft |
| 0x03 | Feinstleckpruefung laeuft |
| 0x04 | Referenzleckmessung 2 laeuft |
| 0x05 | Funktion nicht aktiv |
| 0x06 | Funktion beendet |
| 0x0A | Funktion kann nicht gestartet werden |
| 0x0B | Funktion nicht startbar  --&gt; Ubatt ausserhalb Bereich |
| 0x0C | Funktion nicht startbar  --&gt; Schwankung Referenzstrom zu gross |
| 0x0D | Funktion nicht startbar  --&gt; Elektrische Fehler liegen vor |
| 0x0E | Funktion nicht startbar  --&gt; max. Diagnosedauer erreicht |
| 0x0F | Funktion nicht startbar  --&gt; keine Grobleckfreigabe |
| 0x14 | Funktion wurde abgebrochen |
| 0x15 | Abbruch  --&gt;  Betankung erkannt |
| 0x16 | Abbruch  --&gt;  Tankdeckel geoeffnet |
| 0x17 | Abbruch  --&gt;  Ubatt-Schwankung zu gross |
| 0x18 | Abbruch  --&gt;  Bedingung Kl.15 AUS/EIN erkannt |
| 0xXY | Stagepointer unbekannt |

<a id="table-stagedmtlfreeze"></a>
### STAGEDMTLFREEZE

Dimensions: 23 rows × 2 columns

| STAGE | TEXT |
| --- | --- |
| 0x00 | Funktion laeuft |
| 0x01 | Referenzleckmessung |
| 0x02 | Grobleckpruefung/verlaengerte Grobleckpruefung |
| 0x03 | Feinstleckpruefung |
| 0x04 | Referenzleckmessung 2 |
| 0x0A | Funktion kann nicht gestartet werden |
| 0x0B | Funktion war nicht startbar  --&gt; Ubatt ausserhalb Bereich |
| 0x0C | Funktion war nicht startbar  --&gt; Schwankung Referenzstrom zu gross |
| 0x0D | Funktion war nicht startbar  --&gt; Elektrische Fehler liegen vor |
| 0x0E | Funktion war nicht startbar  --&gt; max. Diagnosedauer erreicht |
| 0x0F | Funktion war nicht startbar  --&gt; keine Grobleckfreigabe |
| 0x14 | Funktion wurde abgebrochen |
| 0x15 | Abbruch  --&gt;  Betankung erkannt |
| 0x16 | Abbruch  --&gt;  Tankdeckel geoeffnet |
| 0x17 | Abbruch  --&gt;  Ubatt-Schwankung zu gross |
| 0x18 | Abbruch  --&gt;  Bedingung Kl.15 AUS/EIN erkannt |
| 0x1E | Funktion beendet, Dicht erkannt |
| 0x1F | Funktion beendet, Feinleck erkannt |
| 0x20 | Funktion beendet, Grobleck erkannt |
| 0x21 | Funktion beendet, Modulfehler erkannt |
| 0x22 | Funktion beendet, kein Grobleck erkannt |
| 0xFF | DM-TL Diagnose noch nie durchlaufen |
| 0xXY | Stagepointer unbekannt |

<a id="table-lsustatus"></a>
### LSUSTATUS

Dimensions: 3 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | LSU Dynamikprüfung wegen Umweltbedingung nicht aktiv |
| 0x01 | LSU Prüfung aktiv |
| 0xXY | LSU Prüfung abgeschlossen  |

<a id="table-lsustatus-neu"></a>
### LSUSTATUS_NEU

Dimensions: 12 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Systemtest noch nicht gestartet wegen fehlender Bedingung oder Fehlereintrag |
| 0x01 | Systemtest für Bank 1 läuft, für Bank 2 noch nicht gestartet |
| 0x02 | Systemtest für Bank 2 läuft, für Bank 1 noch nicht gestartet |
| 0x03 | Systemtest läuft |
| 0x04 | Systemtest für Bank 1 abgeschlossen, für Bank 2 noch nicht gestartet |
| 0x05 | Systemtest für Bank 1 abgeschlossen, Fehler im System auf Bank 2 |
| 0x06 | Systemtest für Bank 2 abgeschlossen, für Bank 1 noch nicht gestartet |
| 0x07 | Systemtest für Bank 2 abgeschlossen, Fehler im System auf Bank 1 |
| 0x08 | Systemtest für Bank 1 abgeschlossen, für Bank 2 noch nicht abgeschlossen |
| 0x09 | Systemtest für Bank 2 abgeschlossen, für Bank 1 noch nicht abgeschlossen |
| 0x10 | Systemtest abgeschlossen |
| 0xFF | Status LSU-Diagnose kann nicht ausgegeben werden |

<a id="table-disastatus"></a>
### DISASTATUS

Dimensions: 9 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | nicht gelernt |
| 0x01 | Lernschritt 1 (Naehe Unterer mech. Anschlag) |
| 0x02 | Lernschritt 2 (Langsames Fahren gegen unteren mech. Anschlag) |
| 0x03 | Lernen erfolgreich beendet |
| 0x04 | Poti MIN- oder MAX-Fehler (Verlassen des Diagnosebereichs) |
| 0x05 | Lagereglerfehler |
| 0x06 | Temperaturwarnung |
| 0x07 | Uebertemperatur Antriebseinheit |
| 0xXY | Status DISA-Diagnose kann nicht ausgegeben werden |

<a id="table-lambdastatus"></a>
### LAMBDASTATUS

Dimensions: 6 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Steuerbetrieb, Startbedingungen noch nicht erfuellt |
| 0x01 | Regelbetrieb mit zwei Sonden |
| 0x02 | Steuerbetrieb durch Betriebsbedingungen |
| 0x04 | Steuerbetrieb nach Systemfehler |
| 0x08 | Regelung mit nur einer Sonde (vor Kat) |
| 0xXY | Status LSU-Diagnose kann nicht ausgegeben werden |

<a id="table-betriebsstundenstatus"></a>
### BETRIEBSSTUNDENSTATUS

Dimensions: 4 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Betriebsstundenzaehler verstanden und akzeptiert (top_w &lt; 10h) |
| 0x01 | Betriebsstundenzaehler verstanden aber nicht akzeptiert (top_w &gt; 10h) |
| 0x02 | Betriebsstundenzaehler nicht verstanden und nicht akzeptiert |
| 0xXY | Betriebsstundenzaehler kann nicht ausgegeben werden |

<a id="table-katstatus"></a>
### KATSTATUS

Dimensions: 7 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Systemtest KAT laeuft |
| 0x01 | Startbedingungen nicht erfüllt |
| 0x05 | Systemtest ist noch nicht gestartet |
| 0x07 | Funktion abgebrochen wegen anderer Fehlereinträge |
| 0x08 | Funktion vollständig durchlaufen, kein Fehler |
| 0x09 | Funktion vollständig durchlaufen, Fehler erkannt |
| 0xXY | Status Systemtest KAT kann nicht ausgegeben werden |

<a id="table-me923-cnv-s-2-def-bit-ub-741-cm"></a>
### _ME923_CNV_S_2_DEF_BIT_UB_741_CM

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Falsch |
| 1 | Wahr |

<a id="table-me923-cnv-s-2-def-bit-ub-755-cm"></a>
### _ME923_CNV_S_2_DEF_BIT_UB_755_CM

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Auslieferungszustand |
| 1 | Abweichung zum Auslieferungszustand |

<a id="table-me923-cnv-s-2-def-bit-ub-755-cm0x2"></a>
### _ME923_CNV_S_2_DEF_BIT_UB_755_CM0X2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Schaltpunktanzeige inaktiv |
| 1 | Schaltpunktanzeige aktiv |

<a id="table-me923-table-st-gentest"></a>
### _ME923_TABLE_ST_GENTEST

Dimensions: 8 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |

<a id="table-me923-table-geniutest-err-bit0"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, elektrischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, elektrischer Fehler Generator vorhanden |

<a id="table-me923-table-geniutest-err-bit1"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, mechanischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, mechanischer Fehler Generator vorhanden |

<a id="table-me923-table-geniutest-err-bit2"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator vorhanden |

<a id="table-me923-table-geniutest-err-bit3"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatortyp plausibel |
| 1 | Generatortest, Generatortyp unplausibel |

<a id="table-me923-table-geniutest-err-bit4"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorkommunikation vorhanden |
| 1 | Generatortest, keine Generatorkommunikation vorhanden |

<a id="table-me923-table-geniutest-err-bit5"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorspannung aus Berechnung plausibel |
| 1 | Generatortest, Generatorspannung aus Berechnung unplausibel |

<a id="table-me923-table-geniutest-err-bit6"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator aus Berechnung nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator aus Berechnung vorhanden |

<a id="table-me923-table-geniutest-err-bit7"></a>
### _ME923_TABLE_GENIUTEST_ERR_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorregler plausibel |
| 1 | Generatortest, Generatorregler unplausibel |

<a id="table-me923-table-geniutest-ab-bit0"></a>
### _ME923_TABLE_GENIUTEST_AB_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorauslastung nicht zu hoch |
| 1 | Generatortest, Generatorauslastung zu hoch |

<a id="table-me923-table-fs"></a>
### _ME923_TABLE_FS

Dimensions: 10 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet (ohne Ergebnis) |
| 7 | Funktion abgebrochen |
| 8 | Funktion vollstaendig durchlaufen und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen und Fehler erkannt |

<a id="table-stat-ruhestrom"></a>
### STAT_RUHESTROM

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 0 keine Ruhestromverletzung, keine Standverbraucher aktiv |
| 0x01 | 1 Ruhestrom 80 bis 200mA aktiv, keine Standverbraucher aktiv |
| 0x02 | 2 Ruhestrom 200 bis 1000mA aktiv, keine Standverbraucher aktiv |
| 0x03 | 3 Ruhestrom über 1000mA aktiv, keine Standverbraucher aktiv |
| 0x04 | 4 keine Ruhestromverletzung, Standverbraucher Licht aktiv |
| 0x05 | 5 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Licht aktiv |
| 0x06 | 6 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x07 | 7 Ruhestrom über 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x08 | 8 keine Ruhestromverletzung, Standverbraucher Standheizung aktiv |
| 0x09 | 9 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0A | 10 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0B | 11 Ruhestrom über 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0C | 12 keine Ruhestromverletzung, Standverbraucher Sonstige aktiv |
| 0x0D | 13 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0E | 14 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0F | 15 Ruhestrom über 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0xFF | 255 Status unbekannt |
