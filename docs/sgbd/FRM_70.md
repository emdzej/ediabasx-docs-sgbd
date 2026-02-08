# FRM_70.prg

- Jobs: [222](#jobs)
- Tables: [50](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | FRM II |
| ORIGIN | BMW EI-63 Alexander Kober |
| REVISION | 4.000 |
| AUTHOR | LEAR DCS Ahrens, LEAR DCS Mesa, Brose Entwicklung-Elektronik Gerstner |
| COMMENT | N/A |
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
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
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
- [STATUS_WIEDERHOLZAEHLER](#job-status-wiederholzaehler) - KWP2000: $30-&gt;IOCBLI, $20 Wiederholzaehler auslesen, $01-&gt;RCS mit dem SGBD-Generator erzeugt
- [STATUS_SPIEGEL_HEIZUNG](#job-status-spiegel-heizung) - KWP2000: $30-&gt;IOCBLI, $20 Spiegel Heizung, $01-&gt;RCS mit dem SGBD-Generator erzeugt
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $01 Digitale Inputs
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 Analoge Inputs
- [STATUS_MEMORY_POSITION_SPIEGEL](#job-status-memory-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0C Position Spiegel fuer FRMFA Status von PL2-FRMFA lesen Abfrage der MemoryPosition der beiden Aussenspiegel
- [STATUS_SCHALTERBLOCK_TUER](#job-status-schalterblock-tuer) - Abfragen der Stati der angeschlossenen Schalterbloecke KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $15 Schalterblock Tuer 
- [STATUS_TUER](#job-status-tuer) - Status-Abfragen Tuer Beinhaltet Fenster, Fensterheber, Spiegel und KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $16 Schalterblock Tuer Zentralverriegelung
- [STATUS_POSITION_SPIEGEL](#job-status-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $10 Position Spiegel fuer FRMFA Status von FRMFA lesen Abfrage der Position der beiden Aussenspiegel
- [STATUS_SPIEGEL_ABBLENDEN](#job-status-spiegel-abblenden) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $11 SPIEGEL_ABBLENDEN Status von FRM-II lesen Auslesen des Wertes, wie der Spiegel abgeblendet ist
- [STATUS_DIMMWERT](#job-status-dimmwert) - KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der digitalen Stati (%) aller Lampen $01-&gt;RCS mit dem SGBD-Generator erzeugt
- [STATUS_LAMPEN_DIGITAL](#job-status-lampen-digital) - KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der digitalen Stati (EIN/AUS) aller Lampen $01-&gt;RCS mit dem SGBD-Generator erzeugt
- [STATUS_SENSE_LESEN](#job-status-sense-lesen) - Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $17 Sensewert Modus  : Default
- [STATUS_INNENBELEUCHTUNG_DAUERAUS](#job-status-innenbeleuchtung-daueraus) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $26 Innenbeleuchtung Daueraus Auslesen, ob Innenlicht daueraus geschaltet wurde
- [STATUS_LAMPEN_DEFEKTE](#job-status-lampen-defekte) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $27 Lampenfehler auslesen Status Defektbits (explizit) von FRM-II lesen
- [STATUS_FLC_FLA_AHL](#job-status-flc-fla-ahl) - Auslesen spezieller Stati KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $28 Stati fuer FLC, FLA und AHL
- [STATUS_FAHRZEUGNEIGUNG](#job-status-fahrzeugneigung) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $30 STATUS_FAHRZEUGNEIGUNG
- [STATUS_KINDERSICHERUNG](#job-status-kindersicherung) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0D Kindersicherung Status von FRMFA lesen Status der Kindersicherung auslesen
- [STATUS_DIMMWERT_LED](#job-status-dimmwert-led) - KWP2000: $30-&gt;IOCBLI $35-&gt;Auslesen der digitalen Stati (%) aller Lampen $01-&gt;RCS mit dem SGBD-Generator erzeugt
- [STATUS_LED_DIGITAL](#job-status-led-digital) - KWP2000: $30-&gt;IOCBLI $35-&gt;Auslesen der digitalen Stati (EIN/AUS) aller LED $01-&gt;RCS mit dem SGBD-Generator erzeugt
- [STATUS_BIXENON_KLAPPE](#job-status-bixenon-klappe) - KWP2000: $30-&gt;IOCBLI $36-&gt;Auslesen der digitalen Stati (EIN/AUS) aller LED $01-&gt;RCS mit dem SGBD-Generator erzeugt
- [STATUS_WARNBLINKEN](#job-status-warnblinken) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 Warnblinken Status von FRM-II lesen Status ob Warnblinken aktiv ist auslesen
- [_FLASH_COMICRO_LEAR](#job-flash-comicro-lear) - Flashen des CoMicro mit Daten aus dem Flash KWP2000: $2E WriteDataByCommonIdentifier $0001 Flash CoMicro
- [_READ_VARIABLE_CO_MICRO_LEAR](#job-read-variable-co-micro-lear) - Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $07 Variable Co-Micro
- [_STEUERN_RESET_COMICRO_WD](#job-steuern-reset-comicro-wd) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1C Reset comicro WatchDog Steuern von FRM II schreiben
- [STEUERN_HW_NOTLAUF](#job-steuern-hw-notlauf) - Loeschen des CoMicro KWP2000: $3B WriteDataByLocalIdentifier $07 Co-Micro
- [_ERASE_COMICRO_LEAR](#job-erase-comicro-lear) - Loeschen des CoMicro KWP2000: $3B WriteDataByLocalIdentifier $07 Co-Micro
- [_CODIERDATEN_BLOCK_LESEN_LEAR](#job-codierdaten-block-lesen-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [_CODIERDATEN_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten Modus  : Codieren je nach Block
- [_CODIERDATEN_3400_LESEN_KOMPLETT_LEAR](#job-codierdaten-3400-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3400-Bereich Auslesen der FRMFA-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3500_LESEN_KOMPLETT_LEAR](#job-codierdaten-3500-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3500-Bereich (FH) KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3000_LESEN_KOMPLETT_LEAR](#job-codierdaten-3000-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3000-Bereich Auslesen der ALC-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3400_SCHREIBEN_AUS_DATEI_LEAR](#job-codierdaten-3400-schreiben-aus-datei-lear) - Beschreiben der Default-Codierdaten Beschreiben der FRMFA-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $34xx Codierdaten, Default Modus  : Default
- [_CODIERDATEN_KOMPLETT_SCHREIBEN_LEAR](#job-codierdaten-komplett-schreiben-lear) - Beschreiben der Default-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten AHL schreiben $31xx Codierdaten Code schreiben $32xx Codierdaten SMC_L schreiben $33xx Codierdaten SMC_R schreiben $34xx Codierdaten FRMFA schreiben $35xx Codierdaten FH schreiben Modus  : Default
- [_I_STUFE_LESEN_LEAR](#job-i-stufe-lesen-lear) - Auslesen der I-Stufe KWP2000: $22 ReadDataByCommonIdentifier $100B I-Step Modus  : Default
- [_I_STUFE_SCHREIBEN_LEAR](#job-i-stufe-schreiben-lear) - Beschreiben der I-Stufe Es muessen immer alle drei Argumente im Bereich von 0-65535 bzw. 0x0000-0xFFFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $100B I-Step Modus  : Default
- [READ_FVIN](#job-read-fvin) - liest die lange Fahrgestellnummer KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN
- [WRITE_FVIN](#job-write-fvin) - schreibt die lange Fahrgestellnummer KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN
- [FVIN_AUFTRAG](#job-fvin-auftrag) - lange Fahrgestellnummer schreiben und ruecklesen KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN
- [_BRIF_SCHREIBEN_LEAR](#job-brif-schreiben-lear) - Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default
- [_BRIF_FILE_LEAR](#job-brif-file-lear) - Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default
- [STATUS_BETR_H_FUNKTIONEN](#job-status-betr-h-funktionen) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Betriebsstunden fuer alle Funktionen Status von FRMFA lesen Lesen der Betriebsstunden der einzelnen Lampenfunktionen des FRM-II
- [STEUERN_BETR_H_LOESCHEN](#job-steuern-betr-h-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Betriebsstunden Status von FRMFA schreiben Loeschen aller Betriebsstunden des FRM-II
- [STATUS_SCHLOSSNUESSE](#job-status-schlossnuesse) - Auslesen der Stati von den Schlossnuessen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Schlossnuesse
- [STATUS_LWR_POSITION](#job-status-lwr-position) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $09 STATUS_LWR_POSITION
- [STATUS_XENON_AL_EINSCHALTVERSUCHE](#job-status-xenon-al-einschaltversuche) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $14 Xenon-AL-Einschaltversuche Auslesen wie oft das Abblendlicht eingeschaltet wurde
- [STEUERN_XENON_AL_EINSCHALTVERSUCHE_LOESCHEN](#job-steuern-xenon-al-einschaltversuche-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $14 Xenon-AL-Einschaltversuche Loeschen der AL-Einschaltversuche
- [STATUS_HOEHENSTAND](#job-status-hoehenstand) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $33 STATUS_HOEHENSTAND Auslesen der Hoehenstandswerte
- [_WARTEZEIT_LEAR](#job-wartezeit-lear) - Wartezeit
- [STATUS_FENSTERHEBER](#job-status-fensterheber) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0A Stati der Fensterheber fuer FRMFA Status vom FRMFA lesen Stati der einzelnen FH-Funktionen auslesen
- [STATUS_EE_FH_LOG_DATA](#job-status-ee-fh-log-data) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA
- [STEUERN_EE_FH_LOG_DATA](#job-steuern-ee-fh-log-data) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $13 EE_FH_LOG_DATA Status von FRMFA schreiben Loeschen von EE_FH_LOG_DATA des FRMFA
- [_STATUS_FH_DENORMIERUNGS_LOGGER_LESEN_LEAR](#job-status-fh-denormierungs-logger-lesen-lear) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA
- [_STEUERN_DIAGNOSE_BROSE_FH_1](#job-steuern-diagnose-brose-fh-1) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1B Diagnose fuer BROSE-FH $01 job 1 Status von FRM-II schreiben
- [_ECHTZEITDATEN_BROSE_LESEN](#job-echtzeitdaten-brose-lesen) - Echtzeitdaten vom Brose auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $18 ECHTZEITDATEN_BROSE_LESEN $01 ReportCurrentState
- [READ_EKS_SUPPLIER](#job-read-eks-supplier) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $32 EKS HERSTELLER und VERSION
- [STATUS_FH_LOGGER_DENORMIERER](#job-status-fh-logger-denormierer) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA
- [STATUS_FH_LOGGER_REVERSIERER](#job-status-fh-logger-reversierer) - Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $2E _STATUS_FH_REVERSIERUNGS_LOGGER_LESEN $01 ReadCurrentState
- [_READ_LINK_DATE_TIME_LEAR](#job-read-link-date-time-lear) - Auslesen der Linkdate und -time KWP2000: $21 ReadDataByLocalIdentifier $01 Linkdate und -time
- [_READ_EMERGENCY_FALLBACK_COUNTER_LEAR](#job-read-emergency-fallback-counter-lear) - Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $02 Fallback Counter
- [_CLR_EMERGENCY_FALLBACK_COUNTER_LEAR](#job-clr-emergency-fallback-counter-lear) - KWP2000: $3B WriteDataByLocalIdentifier $02 NOTLAUF_FALLBACK_COUNTER Modus  : Default
- [_READ_ABS_TIMER_LEAR](#job-read-abs-timer-lear) - Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $09 ABS_TIMER
- [_CLR_ABS_TIMER_LEAR](#job-clr-abs-timer-lear) - KWP2000: $3B WriteDataByLocalIdentifier $09 ABS_TIMER Modus  : Default
- [STATUS_ECU_VARIANTE](#job-status-ecu-variante) - KWP 2000: $21 ReadDataByLocalIdentifier $03 VARIANTE Modus   : Default Auslesen der Variante des Steuergeraetes
- [_HERSTELLER_DATEN_LESEN_LEAR](#job-hersteller-daten-lesen-lear) - Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $04 Herstellerdaten
- [_HERSTELLER_DATEN_SCHREIBEN_LEAR](#job-hersteller-daten-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $3B WriteDataByLocalIdentifier $04 Herstellerdaten
- [STATUS_LWR_LESEN](#job-status-lwr-lesen) - Unterscheidung zwischen dynamischer, automatischer und manueller LWR KWP2000: $21 ReadDataByLocalIdentifier $05 LWR lesen
- [_READ_ENERGY_SAVING_MODE_LEAR](#job-read-energy-saving-mode-lear) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [_CBD_ZEICHN_INDEX_LESEN_LEAR](#job-cbd-zeichn-index-lesen-lear) - Auslesen des Aenderungsindex aus den Codierdaten KWP2000: $21 ReadDataByLocalIdentifier $06 CBD_ZEICHN_INDEX lesen
- [STATUS_SENSE_INPUTS](#job-status-sense-inputs) - Auslesen der Sensewerte der einzelnen Lampen KWP2000: $21 ReadDataByLocalIdentifier $08 Sensewerte lesen
- [STATUS_SENSE_BEREICHE](#job-status-sense-bereiche) - Auslesen der Sensewerte der einzelnen Lampen KWP2000: $21 ReadDataByLocalIdentifier $08 Sensewertebereiche lesen
- [STATUS_PIA_DATEN](#job-status-pia-daten) - Auslesen der momentan aktuellen Piadaten KWP2000: $21 ReadDataByLocalIdentifier $0A Piadaten
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [_RESET_KURZSCHLUSS_SPERRE](#job-reset-kurzschluss-sperre) - Kurzschlusssperre ueber Diagnose ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Kurzschlusssperre ausschalten Status von FRM-II schreiben
- [STATUS_LAMPEN_KURZSCHLUSS](#job-status-lampen-kurzschluss) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $20 Lampenkurzschluss auslesen Status Lampenkurzschluesse (explizit) von FRM-II lesen
- [STATUS_LAMPEN_KURZSCHLUSS_WIEDERHOL_COUNTER](#job-status-lampen-kurzschluss-wiederhol-counter) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $21 Lampenkurzschluss Wiederholzaehler auslesen Status Lampenkurzschlusswiederholzaehler (explizit) von FRM-II lesen
- [STATUS_LAMPEN_KURZSCHLUSS_COUNTER](#job-status-lampen-kurzschluss-counter) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $22 Lampenkurzschluss Zaehler auslesen Status Lampenkurzschlusszaehler (explizit) von FRM-II lesen
- [STATUS_LAMPEN_KURZSCHLUSS_COUNTER_MAX](#job-status-lampen-kurzschluss-counter-max) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $23 Lampenkurzschluss Zaehler Maxwert auslesen Status des max. Wertes des Lampenkurzschlusszaehlers (explizit) von FRM-II lesen
- [STATUS_CODIERBITS](#job-status-codierbits) - Auslesen spezieller Codierbits KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $26 Codierbits
- [STATUS_LENKSTOCK](#job-status-lenkstock) - Status der Lenkstock-Funktionen
- [_STATUS_VAR_IAP_PWR_ASCET_INPUT](#job-status-var-iap-pwr-ascet-input) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A Power Window Ascet Model $00 Input Variables
- [_STATUS_VAR_IAP_PWR_ASCET_OUTPUT](#job-status-var-iap-pwr-ascet-output) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A Power Window Ascet Model $01 Output Variables
- [_STATUS_VAR_IAP_PWR_ASCET_COD](#job-status-var-iap-pwr-ascet-cod) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A Power Window Ascet Model $02 Coding Variables
- [_STATUS_VAR_IAP_PWR_BROSE_GLOBALVAR_FAT](#job-status-var-iap-pwr-brose-globalvar-fat) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $00 Global Variables FAT
- [_STATUS_VAR_IAP_PWR_BROSE_GLOBALVAR_BFT](#job-status-var-iap-pwr-brose-globalvar-bft) - Auslesen der Stati von den Internen Variablen Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $01 Global Variables BFT
- [_STATUS_VAR_IAP_PWR_BROSE_GLOBALFLG_FAT](#job-status-var-iap-pwr-brose-globalflg-fat) - Auslesen der Stati von den Internen Variablen Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $02 Global Flags FAT
- [_STATUS_VAR_IAP_PWR_BROSE_GLOBALFLG_BFT](#job-status-var-iap-pwr-brose-globalflg-bft) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $03 Global Flags BFT
- [_STATUS_VAR_IAP_PWR_BROSE_CONTROL_FAT](#job-status-var-iap-pwr-brose-control-fat) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $04 Control Variables FAT
- [_STATUS_VAR_IAP_PWR_BROSE_CONTROL_BFT](#job-status-var-iap-pwr-brose-control-bft) - Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $05 Control Variables BFT
- [STEUERN_FH_ADAPTIONSSPEICHER_LOESCHEN](#job-steuern-fh-adaptionsspeicher-loeschen) - Adaptionsdaten Fensterheber Loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $2C FH Adaptation Speicher loeschen $07 ShortTermAdjustment
- [_MARGINAL_READ_FLASH](#job-marginal-read-flash) - Read out of marginal read compress value for flashROM KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $34 Marginal Read Flash
- [_READ_DIAG_RINGSPEICHER](#job-read-diag-ringspeicher) - KWP 2000: $21 ReadDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus   : Default
- [_CLR_DIAG_RINGSPEICHER_LEAR](#job-clr-diag-ringspeicher-lear) - KWP2000: $3B WriteDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus  : Default
- [_READ_DIAG_RINGSPEICHER_RESET](#job-read-diag-ringspeicher-reset) - KWP 2000: $21 ReadDataByLocalIdentifier $0C DIAG_RESETSPEICHER Modus   : Default
- [_CLR_DIAG_RESETPEICHER_LEAR](#job-clr-diag-resetpeicher-lear) - KWP2000: $3B WriteDataByLocalIdentifier $0C DIAG_RESETSPEICHER Modus  : Default
- [READ_ENERGY_OUTPUT](#job-read-energy-output) - Read out the energy output data KWP 2000: $21 ReadDataByLocalIdentifier $0D ENERGY_OUTPUT Modus   : Default
- [STATUS_QUALITAET_FENSTERHEBERLAUF](#job-status-qualitaet-fensterheberlauf) - Qualitaetsbewertung Fensterheber
- [_STATUS_FH_ADAPTIONSSPEICHER_LESEN](#job-status-fh-adaptionsspeicher-lesen) - Adaptionsdaten Fensterheber KWP2000: $30 InputOutputControlByLocalIdentifier $18 ECHTZEITDATEN_BROSE_LESEN $01 ReportCurrentState
- [_STATUS_FH_REVERSIERUNGS_LOGGER_LESEN_LEAR](#job-status-fh-reversierungs-logger-lesen-lear) - Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $2E _STATUS_FH_REVERSIERUNGS_LOGGER_LESEN $01 ReadCurrentState
- [_STEUERN_FH_REVERSIERUNGS_LOGGER_LOESCHEN_LEAR](#job-steuern-fh-reversierungs-logger-loeschen-lear) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2E Reversierungslogger Status von FRMFA schreiben Loeschen von Reversierungslogger des FRMFA
- [STEUERN_LAMPEN_DIGITAL](#job-steuern-lampen-digital) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von FRM II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten
- [STEUERN_LAMPEN_PWM](#job-steuern-lampen-pwm) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von FRM II schreiben Lampe mit Prozentwert ein- bzw. ausschalten
- [STEUERN_KINDERSICHERUNG](#job-steuern-kindersicherung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0D Kindersicherung Status von FRMFA schreiben Betaetigung des Kindersicherungstasters simulieren
- [_STEUERN_SPIEGELHEIZUNG_LEAR](#job-steuern-spiegelheizung-lear) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0E Spiegelheizung Status von FRM-II schreiben Spiegelheizung mit speziellen Werten eischalten
- [STEUERN_SPIEGEL_POSITION](#job-steuern-spiegel-position) - Ansteuerung Spiegel Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen
- [STEUERN_SPIEGEL_HEIZUNG](#job-steuern-spiegel-heizung) - Ein bzw. Ausschalten der Spiegelheizung per Diagnose
- [STEUERN_SPIEGEL_ABBLENDEN](#job-steuern-spiegel-abblenden) - Ein bzw. Ausschalten der Spiegelheizung per Diagnose Max. Dauer 6 Sekunden mit ca. 60%
- [STEUERN_DIGITAL_TUER](#job-steuern-digital-tuer) - Ansteuerung der digitalen Eingaenge der Tuer
- [STEUERN_FENSTERHEBER](#job-steuern-fensterheber) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0A Ansteuern FH Status von FRMFA schreiben Verfahren der Fensterheber, Fahrer, Beifahrer, beide
- [STEUERN_FENSTERHEBER_EINLERNEN_OHNE_EKS](#job-steuern-fensterheber-einlernen-ohne-eks) - Einlernen der Fensterheber Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen
- [STEUERN_FENSTERHEBER_EINLERNEN](#job-steuern-fensterheber-einlernen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $19 Ansteuern FH Status von FRM II schreiben Dauer max. 7sec Einlernen der Fensterheber mit EKS
- [STEUERN_FENSTERHEBER_DENORMIEREN](#job-steuern-fensterheber-denormieren) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $19 Ansteuern FH Status von FRM II schreiben Dauer max. 7sec Einlernen der Fensterheber
- [STEUERN_AL_EINSCHALTEN](#job-steuern-al-einschalten) - Abblendlicht ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0F Abblendlicht ein- bzw. ausschalten Status von FRMFA schreiben
- [STEUERN_LAMPEN_FUNKTIONEN_EINSCHALTEN](#job-steuern-lampen-funktionen-einschalten) - Lampenfunktionen ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $29 Lampenfunktionen ein- bzw. ausschalten Status von FRMFA schreiben
- [STEUERN_POSITION_DIREKT_SPIEGEL](#job-steuern-position-direkt-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $12 Position Spiegel fuer FRMFA Status von FRM-II schreiben ausgewaehlten Spiegel in angegebene Position fahren
- [_STEUERN_SPIEGEL_ABBLENDEN_LEAR](#job-steuern-spiegel-abblenden-lear) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $11 SPIEGEL_ABBLENDEN Status von FRM-II schreiben Abblenden der Aussenspiegel
- [STEUERN_MEMORY_POSITION_SPIEGEL](#job-steuern-memory-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0C Position Spiegel fuer FRMFA Status von PL4-FRM II schreiben Schreiben der MemoryPosition der beiden Aussenspiegel
- [STEUERN_INNENBELEUCHTUNG_DAUERAUS](#job-steuern-innenbeleuchtung-daueraus) - KWP2000: $30 InputOutputControlByLocalIdentifier $08 LongTermAdjustment $26 Innenbeleuchtung Dauerausschalten Innenbeleuchtung Dauerausschalten
- [STEUERN_FENSTERHEBER_MESSDATEN_AKTIVIEREN](#job-steuern-fensterheber-messdaten-aktivieren) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1E Ansteuern FH Messdatenausgabe fuer FH starten
- [STEUERN_BFD_STUFE](#job-steuern-bfd-stufe) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $24 BFD-Stufe ein-/ausschalten Status von FRM II schreiben Ausgewaehlte BFD-Stufe ein bzw. ausschalten
- [STEUERN_POSITION_LWR](#job-steuern-position-lwr) - bestimmte Position der LWR anfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $09 Position der LWR anfahren Status von FRM II schreiben
- [STEUERN_KURZHUB_DEAKTIVIEREN](#job-steuern-kurzhub-deaktivieren) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2D Kurzhub Deaktivieren
- [STEUERN_INNENBELEUCHTUNG](#job-steuern-innenbeleuchtung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2F Innenbeleuchtung Status von FRMFA schreiben
- [START_LAMPEN_PRE_DRIVE_CHECK](#job-start-lampen-pre-drive-check) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $31 Start des Pre-Drive-Checks der Lampen Status von FRMFA schreiben
- [STEUERN_LED_DIGITAL](#job-steuern-led-digital) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $35 Dimmwert an LED Status von FRM II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten
- [STEUERN_LED_PWM](#job-steuern-led-pwm) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $35 Dimmwert an PWM-Port Status von FRM II schreiben Lampe mit Prozentwert ein- bzw. ausschalten
- [STEUERN_BIXENON_KLAPPE_DIGITAL](#job-steuern-bixenon-klappe-digital) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $36 Dimmwert an LED Status von FRM II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten
- [STEUERN_SMC_BESTROMEN](#job-steuern-smc-bestromen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1A SMC bestromen Status von FRM-II schreiben Bestromung der SMCs einschalten
- [STEUERN_REFERENZLAUF_ALC_SYSTEM](#job-steuern-referenzlauf-alc-system) - Referenzlauf der SMCs starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten
- [STATUS_REFERENZLAUF_ALC_SYSTEM](#job-status-referenzlauf-alc-system) - Pruefung, ob ALC-System referenziert ist KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR
- [_CODIERDATEN_SMC_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-smc-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier $xxxx Codierdaten schreiben Modus  : Codieren je nach Block
- [_CODIERDATEN_SMC_SCHREIBEN_LEAR](#job-codierdaten-smc-schreiben-lear) - Beschreiben der Default-Codierdaten KWP 2000:$A6 LINGateway $2E WriteDataByCommonIdentifier $32xx Codierdaten SMC links schreiben $33xx Codierdaten SMC rechts schreiben Modus  : Default
- [_CODIERDATEN_SMC_BLOCK_LESEN_LEAR](#job-codierdaten-smc-block-lesen-lear) - Auslesen der Codierdaten fuer einen Block KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x32xx Codierdaten SMC links schreiben $0x33xx Codierdaten SMC rechts schreiben Modus  : Default
- [_CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-links-lesen-komplett-lear) - Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $32xx Codierdaten SMC links lesen Modus  : Default
- [_CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-rechts-lesen-komplett-lear) - Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $33xx Codierdaten SMC rechts lesen Modus  : Default
- [VIN_SMC_LINKS_SCHREIBEN_LEAR](#job-vin-smc-links-schreiben-lear) - Schreiben der VIN in die linke SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die linke SMC
- [VIN_SMC_RECHTS_SCHREIBEN_LEAR](#job-vin-smc-rechts-schreiben-lear) - Schreiben der VIN in die rechte SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die rechte SMC
- [VIN_SMC_LESEN](#job-vin-smc-lesen) - Fahrgestellnummer fuer SMC links und rechts lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [ID_SMC_LESEN](#job-id-smc-lesen) - ID-SMC lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-SMC Modus  : Default Auslesen der Identdaten der SMCs
- [STEUERN_REFERENZLAUF_SMC](#job-steuern-referenzlauf-smc) - Referenzlauf der SMC starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten
- [STATUS_POSITION_SMC](#job-status-position-smc) - IST-Position der SMC auslesen KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR
- [STEUERN_POSITION_SMC](#job-steuern-position-smc) - bestimmte Position der SMC anfahren KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht starten $41 Pos LWR starten
- [SMC_SPEICHER_LESEN_LEAR](#job-smc-speicher-lesen-lear) - Speicher lesen KWP 2000: $A6 LINGateway $23 ReadMemoryByAddress Modus  : Default
- [SMC_SPEICHER_SCHREIBEN_LEAR](#job-smc-speicher-schreiben-lear) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Start-Adresse Datenbyte KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [_HERSTELLERDATEN_SMC_LEAR_SCHREIBEN](#job-herstellerdaten-smc-lear-schreiben) - Beschreiben der LEAR-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [_HERSTELLERDATEN_SMC_LEAR_LESEN](#job-herstellerdaten-smc-lear-lesen) - Auslesen der LEAR-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3280 Herstellerdaten SMC links lesen $0x3380 HErstellerdaten SMC rechts lesen Modus  : Default
- [HERSTELLERDATEN_SMC_SCHEINWERFER_SCHREIBEN](#job-herstellerdaten-smc-scheinwerfer-schreiben) - Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [HERSTELLERDATEN_SMC_SCHEINWERFER_LESEN](#job-herstellerdaten-smc-scheinwerfer-lesen) - Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default
- [IS_LESEN_SMC_L_LEAR](#job-is-lesen-smc-l-lear) - Infospeicher von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_SMC_R_LEAR](#job-is-lesen-smc-r-lear) - Infospeicher von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL_SMC_L_LEAR](#job-is-lesen-detail-smc-l-lear) - Infospeicher Details von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LESEN_DETAIL_SMC_R_LEAR](#job-is-lesen-detail-smc-r-lear) - Infospeicher Details von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN_SMC_L_LEAR](#job-is-loeschen-smc-l-lear) - Infospeicher der SMC links loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [IS_LOESCHEN_SMC_R_LEAR](#job-is-loeschen-smc-r-lear) - Infospeicher der SMC rechts loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [STATUS_BETR_H_SMC](#job-status-betr-h-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $51 Betriebsstunden Betriebsstunden von ausgewaehlter SMC lesen
- [STEUERN_BETR_H_SMC_LOESCHEN](#job-steuern-betr-h-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $51 Betriebsstunden alle Betriebszeiten der ausgewaehlten SMC loeschen
- [STATUS_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC](#job-status-verteilung-winkel-ansteuerung-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $50 Verteilung der Winkelansteuerung Verteilung der Winkelansteuerung von ausgewaehlter SMC lesen
- [STEUERN_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC_LOESCHEN](#job-steuern-verteilung-winkel-ansteuerung-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $50 Verteilung der Winkelansteuerung Loeschen der Verteilung der Winkelansteuerung der ausgewaehlten SMC
- [STATUS_TEMPERATURVERTEILUNG_SMC](#job-status-temperaturverteilung-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $52 Temperaturverteilung Temperaturverteilung von der ausgewaehlten SMC lesen
- [STEUERN_TEMPERATURVERTEILUNG_SMC_LOESCHEN](#job-steuern-temperaturverteilung-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $52 Temperaturverteilung Loeschen der Temperaturverteilung der ausgewaehlten SMC
- [STATUS_SCHRITTVERLUSTE_SMC](#job-status-schrittverluste-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $53 Schrittverluste Schrittverluste von der ausgewaehlten SMC lesen
- [STEUERN_SCHRITTVERLUSTE_SMC_LOESCHEN](#job-steuern-schrittverluste-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $53 Schrittverluste Loeschen der Schrittverluste der ausgewaehlten SMC
- [STATUS_HW_EINGANGE_SMC](#job-status-hw-eingange-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $54 HW_Eingaenge HW_Eingaenge von der ausgewaehlten SMC lesen
- [_HERSTELLERTEST_SMC_LEAR](#job-herstellertest-smc-lear) - Herstellertest KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $04 Herstellertest Modus  : Default
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

<a id="job-status-wiederholzaehler"></a>
### STATUS_WIEDERHOLZAEHLER

KWP2000: $30-&gt;IOCBLI, $20 Wiederholzaehler auslesen, $01-&gt;RCS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WIEDERHOLZAEHLER_ASP_BEIKLAPPEN_WERT | real | Wiederholzaehler Aussenspiegel Beiklappen auslesen Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_WIEDERHOLZAEHLER_ASP_BEIKLAPPEN_EINH | string | Wiederholzaehler Aussenspiegel Beiklappen auslesen Einheit: 0-n |
| STAT_WIEDERHOLZAEHLER_VORFELDBELEUCHTUNG_WERT | real | Wiederholzaehler Vorfeldbeleuchtung auslesen Bereich von 0 [0-n] bis 65535 [0-n] |
| STAT_WIEDERHOLZAEHLER_VORFELDBELEUCHTUNG_EINH | string | Wiederholzaehler Vorfeldbeleuchtung auslesen Einheit: 0-n |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spiegel-heizung"></a>
### STATUS_SPIEGEL_HEIZUNG

KWP2000: $30-&gt;IOCBLI, $20 Spiegel Heizung, $01-&gt;RCS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPIEGELHEIZUNG_WERT | int | Spiegelheizungposition wert. table SpiegelHeizungStat WERT |
| STAT_SPIEGELHEIZUNG_TEXT | string | Spiegelheizungposition wert. table SpiegelHeizungStat TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $01 Digitale Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTER_LICHT_2_RED_EIN | int | Lichtschalterstellung 2 Redundant ein |
| STAT_EINGANG_R_GANG_EIN | int | Rueckwaertsgang ein |
| STAT_EINGANG_BLS_EIN | int | Bremslichtschalter ein |
| STAT_TASTER_IB_EIN | int | Taster Innenbeleuchtung ein |
| STAT_KLEMME_15_EIN | int | Klemme 15 ein |
| STAT_TASTER_WBL_EIN | int | Taster Warnblinklicht betaetigt |
| STAT_HS_FA_INC1_EIN | int | Hallsensor Fahrertuer Inkrementalgeber 1 ein |
| STAT_HS_FA_INC2_EIN | int | Hallsensor Fahrertuer Inkrementalgeber 2 ein |
| STAT_HS_BFT_INC1_EIN | int | Hallsensor Beifahrertuer Inkrementalgeber 1 ein |
| STAT_HS_BFT_INC2_EIN | int | Hallsensor Beifahrertuer Inkrementalgeber 2 ein |
| STAT_TASTER_FH_FA_DAUER_ZU_EIN | int | Dauer-Taster Fensterheber Fahrertuer zu ein |
| STAT_TASTER_FH_FA_TIPP_ZU_EIN | int | Tipp-Taster Fensterheber Fahrertuer zu ein |
| STAT_TASTER_FH_FA_DAUER_AUF_EIN | int | Dauer-Taster Fensterheber Fahrertuer auf ein |
| STAT_TASTER_FH_FA_TIPP_AUF_EIN | int | Tipp-Taster Fensterheber Fahrertuer auf ein |
| STAT_TASTER_FH_BFT_DAUER_ZU_EIN | int | Dauer-Taster Fensterheber Beifahrertuer zu ein |
| STAT_TASTER_FH_BFT_TIPP_ZU_EIN | int | Tipp-Taster Fensterheber Beifahrertuer zu ein |
| STAT_TASTER_FH_BFT_DAUER_AUF_EIN | int | Dauer-Taster Fensterheber Beifahrertuer auf ein |
| STAT_TASTER_FH_BFT_TIPP_AUF_EIN | int | Tipp-Taster Fensterheber Beifahrertuer auf ein |
| STAT_SCHALTER_FRA_RECHTS_DAUER_EIN | int | Dauer-Schalter Fahrtrichtungsanzeiger rechts ein |
| STAT_SCHALTER_FRA_RECHTS_TIPP_EIN | int | Tipp-Schalter Fahrtrichtungsanzeiger rechts ein |
| STAT_SCHALTER_FRA_LINKS_DAUER_EIN | int | Dauer-Schalter Fahrtrichtungsanzeiger links ein |
| STAT_SCHALTER_FRA_LINKS_TIPP_EIN | int | Tipp-Schalter Fahrtrichtungsanzeiger links ein |
| STAT_SCHALTER_FL_EIN | int | Schalter Fernlicht ein |
| STAT_SCHALTER_LH_EIN | int | Taster Lichthupe ein |
| STAT_TASTER_NSW_EIN | int | Taster Nebelscheinwerfer betaetigt |
| STAT_TASTER_NSL_EIN | int | Taster Nebelschlussleuchte betaetigt |
| STAT_SCHALTER_SL_EIN | int | Schalter Standlicht ein |
| STAT_SCHALTER_AL_EIN | int | Schalter Abblendlicht ein |
| STAT_SCHALTER_FLC_EIN | int | Schalter Fahrlichtkontrolle ein |
| STAT_EINGANG_TK_VL_EIN | int | Tuerkontakt vorne links ein bitte result: STAT_EINGANG_TK_FAT_EIN verwenden |
| STAT_EINGANG_TK_VR_EIN | int | Tuerkontakt vorne rechts ein bitte result: STAT_EINGANG_TK_BFT_EIN verwenden |
| STAT_EINGANG_TK_HL_EIN | int | Tuerkontakt hinten links ein bitte result: STAT_EINGANG_TK_FATH_EIN verwenden |
| STAT_EINGANG_TK_HR_EIN | int | Tuerkontakt hinten rechts ein bitte result: STAT_EINGANG_TK_BFTH_EIN verwenden |
| STAT_EINGANG_TK_FAT_EIN | int | Tuerkontakt Fahrertuer ein |
| STAT_EINGANG_TK_BFT_EIN | int | Tuerkontakt Beifahrertuer ein |
| STAT_EINGANG_TK_FATH_EIN | int | Tuerkontakt Fahrertuer hinten ein |
| STAT_EINGANG_TK_BFTH_EIN | int | Tuerkontakt Beifahrertuer hinten ein |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-inputs"></a>
### STATUS_ANALOG_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 Analoge Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_SCHALTER_FH_FA_WERT | real | Spannung Schalter FH Fahrer Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_FH_BF_WERT | real | Spannung Schalter FH Beifahrer Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_KLEMME_30A_FH_WERT | real | Spannung Klemme 30A FH Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_KLEMME_30B_FH_WERT | real | Spannung Klemme 30B FH Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_KLEMME_30A_WERT | real | Spannung Klemme 30A Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_KLEMME_30B_WERT | real | Spannung Klemme 30B Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_MOTOR_FH_LINKS_WERT | real | Spannung Motor Fensterheber links Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_MOTOR_FH_RECHTS_WERT | real | Spannung Motor Fensterheber rechts Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_HINTEN_WERT | real | Spannung Hoehenstandssensor hinten Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_TASTER_NSW_NSL_WERT | real | Spannung Taster NSW und NSL Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_WERT | real | Spannung Hoehenstandssensor vorne Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_LICHT_1_WERT | real | Spannung Lichtschalterstellung 1 (Standlicht) Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_POTI_5V_WERT | real | Spannung Poti 5 Volt. Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SENSOR_LWR_WERT | real | Spannung LWR Sensor Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_SCHALTER_LICHT_2_WERT | real | Spannung Lichtschalterstellung 2 (Abblendlicht) Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_FRA_LINKS_WERT | real | Spannung Schalter Fahrtrichtungsanzeiger links Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_FL_LH_WERT | real | Spannung Schalter Fernlicht / Lichthupe Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_FRA_RECHTS_WERT | real | Spannung Schalter Fahrtrichtungsanzeiger rechts Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_LWR_POTI_WERT | real | Spannung LWR-Poti Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_DIMMER_POTI_WERT | real | Spannung Dimmer-Poti Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-memory-position-spiegel"></a>
### STATUS_MEMORY_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0C Position Spiegel fuer FRMFA Status von PL2-FRMFA lesen Abfrage der MemoryPosition der beiden Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY | int | 0 bis 3 und 255 welcher Schluessel |
| MEM_POS_SLOT | int | 0 bis 3 welche Memoryposition |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_WERT | int | abgefragter Schluessel |
| STAT_MEM_POS_SLOT_WERT | int | abgefragter Memorypositionsslot |
| STAT_MEM_POS_SPIEGEL_FAHRER_HOR_WERT | int | Position Fahrerspiegel horizontal |
| STAT_MEM_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Position Beifahrerspiegel horizontal |
| STAT_MEM_POS_SPIEGEL_FAHRER_VER_WERT | int | Position Fahrerspiegel vertikal |
| STAT_MEM_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Position Beifahrerspiegel vertikal |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schalterblock-tuer"></a>
### STATUS_SCHALTERBLOCK_TUER

Abfragen der Stati der angeschlossenen Schalterbloecke KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $15 Schalterblock Tuer 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FH_TASTERFA_FA_ZU | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FA_AUF | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FA_MAUT_ZU | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_FA_MAUT_AUF | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_FA_WERT | int | Fahrerseite (Tastenblock) Fensterheber Fahrerseite 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_FH_TASTERFA_BF_ZU | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BF_AUF | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BF_MAUT_ZU | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BF_MAUT_AUF | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BF_WERT | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
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
| STAT_FH_TASTERFA_BFH_ZU | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten zu (Fenster schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BFH_AUF | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten auf (Fenster oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BFH_MAUT_ZU | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten Maut zu (Fenster komplett schliessen) 0: Taster nicht gezogen 1: Taster gezogen |
| STAT_FH_TASTERFA_BFH_MAUT_AUF | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten Maut auf (Fenster komplett oeffnen) 0: Taster nicht gedrueckt 1: Taster gedrueckt |
| STAT_FH_TASTERFA_BFH_WERT | int | Fahrerseite (Tastenblock) Fensterheber Beifahrerseite hinten 0: Taster nicht gedrueckt 1: Fenster schliessen 2: Fenster oeffnen 3: Fenster Maut schliessen 4: Fenster Maut oeffnen |
| STAT_KISI_TASTER_EIN | int | 0: Taster Kindersicherung nicht gedrueckt 1: Taster Kindersicherung gedrueckt |
| STAT_KISI_LED_EIN | int | 0: LED Kindersicherung aus 1: LED Kindersicherung ein |
| STAT_SPIEGEL_SCHALTER_FA_EIN | int | Fahrerseite (Tastenblock) Spiegelauswahl Fahrerseite, Beifahrerseite 0: Beifahrerspiegel 1: Fahrerspiegel |
| STAT_SPIEGEL_BEIKLAPPEN_EIN | int | Fahrerseite (Tastenblock) 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel beizuklappen |
| STAT_SPIEGEL_TASTER_LINKS_EIN | int | Fahrerseite (Tastenblock) 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach links zu bewegen |
| STAT_SPIEGEL_TASTER_RECHTS_EIN | int | Fahrerseite (Tastenblock) 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach rechts zu bewegen |
| STAT_SPIEGEL_TASTER_OBEN_EIN | int | Fahrerseite (Tastenblock) 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach oben zu bewegen |
| STAT_SPIEGEL_TASTER_UNTEN_EIN | int | Fahrerseite (Tastenblock) 0: Taster nicht gedrueckt 1: Taster gedrueckt, um Spiegel nach unten zu bewegen |
| STAT_SPIEGEL_TASTER_WERT | int | Fahrerseite (Tastenblock) 0: Taster nicht gedrueckt 1: Taster links gedrueckt 2: Taster oben gedrueckt 3: Taster rechts gedrueckt 4: Taster unten gedrueckt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tuer"></a>
### STATUS_TUER

Status-Abfragen Tuer Beinhaltet Fenster, Fensterheber, Spiegel und KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $16 Schalterblock Tuer Zentralverriegelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UBATT_WERT | real | (Klemme 30) Spannung am Steuergeraet in Volt Aufloesung ?,?? V/Bit |
| STAT_UBATT_EINH | string | (Klemme 30) Spannung am Steuergeraet in Volt Fensterheber Fahrerseite zu (Fenster schliessen) Aufloesung ?,?? V/Bit |
| STAT_UBATT_LOW | int | 0: Keine Unterspannung detektiert 1: Unterspannung (&lt;12V) an Klemme 30 detektiert (min. Spannung für das Einlernen der Fenster) |
| STAT_UBATT_OVR | int | 0: Keine Ueberspannung detektiert 1: Ueberspannung (&gt;16V) an Klemme 30 detektiert |
| STAT_FH_FA_OFFEN_KOMPLETT | int | Fenster Fahrer komplett offen 0: geschlossen oder halb offen 1: komplett offen |
| STAT_FH_FA_GESCHLOSSEN_KOMPLETT | int | Fenster Fahrerseite komplett geschlossen 0: offen oder halb geschlossen 1: komplett geschlossen |
| STAT_FH_FA_FAEHRT_AUF | int | 0: - 1: Fensterheber Fahrer faehrt auf |
| STAT_FH_FA_FAEHRT_ZU | int | 0: - 1: Fensterheber Fahrer faehrt zu |
| STAT_FH_FA_EINLERNENVORGANG_AKTIV | int | 0: Einlernvorgang (Fensterheber Fahrerseite) nicht aktiv 1: Einlernvorgang (Fensterheber Fahrerseite) aktiv |
| STAT_FH_FA_EINGELERNT | int | 0: Fensterheber Fahrerseite nicht eingelernt 1: Fensterheber Fahrerseite eingelernt |
| STAT_FH_FA_POSITION_WERT | int | Position Fensterheber Fahrerseite, nur bei eingelerntem FH 0: Fenster im ungueltiger Zustand 1: Fenster im gueltigen Zustand (max. Wert bei Fenster geschlossen) Max: &lt;Ist im Kommentar anzugeben&gt; |
| STAT_FH_FA_POSITION_EINH | string | Einheit Position Fensterheber Fahrer |
| STAT_FH_BF_OFFEN_KOMPLETT | int | Fenster Beifahrerseite komplett offen 0: geschlossen oder halb offen 1: komplett offen |
| STAT_FH_BF_GESCHLOSSEN_KOMPLETT | int | Fenster Beifahrerseite komplett geschlossen 0: offen oder halb geschlossen 1: komplett geschlossen |
| STAT_FH_BF_FAEHRT_AUF | int | 0: - 1: Fensterheber Beifahrerseite faehrt auf |
| STAT_FH_BF_FAEHRT_ZU | int | 0: - 1: Fensterheber Beifahrerseite faehrt zu |
| STAT_FH_BF_EINLERNENVORGANG_AKTIV | int | 0: Einlernvorgang (Fensterheber Beifahrerseite) nicht aktiv 1: Einlernvorgang (Fensterheber Beifahrerseite) aktiv |
| STAT_FH_BF_EINGELERNT | int | 0: Fensterheber Beifahrerseite nicht eingelernt 1: Fensterheber Beifahrerseite eingelernt |
| STAT_FH_BF_POSITION_WERT | int | Position Fensterheber Beifahrer, nur bei eingelerntem FH 0: Fenster ungueltiger Zustand 1: Fenster im gueltigen Zustand (max. &lt;Wert bei Fenster geschlossen&gt;) Max: &lt;Ist im Kommentar anzugeben&gt; |
| STAT_FH_BF_POSITION_EINH | string | Einheit Position Fensterheber Beifahrerseite |
| STAT_SPIEGEL_POSHOR_FA_WERT | int | Spiegelposition Fahrerseite horizontal Bereich: ?-?? Inkremente |
| STAT_SPIEGEL_POSHOR_FA_EINH | string | Einheit Spiegelposition Fahrerseite horizontal |
| STAT_SPIEGEL_POSVERT_FA_WERT | int | Spiegelposition Fahrerseite vertikal Bereich: ?-?? Inkremente |
| STAT_SPIEGEL_POSVERT_FA_EINH | string | Einheit Spiegelposition Fahrerseite vertikal |
| STAT_SPIEGEL_POSHOR_BF_WERT | int | Spiegelposition Beifahrerseite horizontal Bereich: ?-?? Inkremente |
| STAT_SPIEGEL_POSHOR_BF_EINH | string | Einheit Spiegelposition Beifahrerseite horizontal |
| STAT_SPIEGEL_POSVERT_BF_WERT | int | Spiegelposition Beifahrerseite vertikal Bereich: ?-?? Inkremente |
| STAT_SPIEGEL_POSVERT_BF_EINH | string | Einheit Spiegelposition Beifahrerseite vertikal |
| STAT_SPIEGEL_BEIGEKLAPPT | int | 0: Spiegel ausgeklappt 1: Spiegel beigeklappt |
| STAT_SPIEGEL_ABGEKLAPPT | int | 0: Spiegel nicht in abgeklappter Bordsteinposition 1: Spiegel in abgeklappter Bordsteinposition |
| STAT_SPIEGEL_HEIZUNG_EIN | int | 0: Spiegelheizung ausgeschaltet 1: Spiegelheizung eingeschaltet |
| STAT_SPIEGEL_ABBLEND_WERT | int | 0: Spiegel nicht abgeblendet 1: Spiegel abgeblendet Achtung: Status steht nur fuer 6 Sekunden zur Verfuegung.Spiegel wird nur mit ca. 60% abgeblendet |
| STAT_SPIEGEL_ABBLEND_EINH | string | % |
| STAT_SPIEGEL_ABBLEND_MOEGLICH | int | 0: Spiegel kann nicht ageblendet werden 1: Spiegel kann abgeblendet werden |
| STAT_SPIEGEL_MIT_MEMORY | int | 0: Spiegel ohne Memoryfunktion 1: Spiegel mit Memoryfunktion |
| STAT_KISI_FH_FAH_AKTIV | int | 0: Kindersicherung Fensterheber und Sonnenrollo Fahrer hinten sind nicht gesperrt 1: Kindersicherung Fensterheber und Sonnenrollo Fahrer hinten sind gesperrt. D.h. sie können nur vom Fahrer aus gesteuert werden |
| STAT_KISI_FH_BFH_AKTIV | int | 0: Kindersicherung Fensterheber und Sonnenrollo Beifahrer hinten sind nicht gesperrt 1: Kindersicherung Fensterheber und Sonnenrollo Beifahrer hinten sind gesperrt. D.h. sie können nur vom Fahrer aus gesteuert werden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-position-spiegel"></a>
### STATUS_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $10 Position Spiegel fuer FRMFA Status von FRMFA lesen Abfrage der Position der beiden Aussenspiegel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_POS_SPIEGEL_FAHRER_HOR_WERT | int | Position Fahrerspiegel horizontal |
| STAT_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Position Beifahrerspiegel horizontal |
| STAT_POS_SPIEGEL_FAHRER_VER_WERT | int | Position Fahrerspiegel vertikal |
| STAT_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Position Beifahrerspiegel vertikal |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spiegel-abblenden"></a>
### STATUS_SPIEGEL_ABBLENDEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $11 SPIEGEL_ABBLENDEN Status von FRM-II lesen Auslesen des Wertes, wie der Spiegel abgeblendet ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPIEGEL_ABBLENDEN_WERT | int | Wert fuer Spiegel abblenden in Prozent von 0 bis 100 255 bedeutet ungueltig |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dimmwert"></a>
### STATUS_DIMMWERT

KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der digitalen Stati (%) aller Lampen $01-&gt;RCS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_WERT | real | Fernlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FL_RECHTS_WERT | real | Fernlicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_AL_LINKS_WERT | real | Abblendlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_AL_RECHTS_WERT | real | Abblendlicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BEGRL_LINKS_WERT | real | Begrenzungslicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BEGRL_RECHTS_WERT | real | Begrenzungslicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSW_LINKS_WERT | real | Nebelscheinwerfer links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSW_RECHTS_WERT | real | Nebelscheinwerfer rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_LINKS_VORN_WERT | real | Fahrtrichtungsanzeiger links vorne Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_RECHTS_VORN_WERT | real | Fahrtrichtungsanzeiger rechts vorne Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_LINKS_HINTEN_WERT | real | Fahrtrichtungsanzeiger links hinten Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_WERT | real | Fahrtrichtungsanzeiger rechts hinten Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BREMSLICHT_LINKS_WERT | real | Bremslicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BREMSLICHT_MITTE_WERT | real | Bremslicht mitte Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BREMSLICHT_RECHTS_WERT | real | Bremslicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_SL_BL_LINKS_1_WERT | real | Schlusslicht links 1 Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_SL_BL_RECHTS_1_WERT | real | Schlusslicht rechts 1 Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_E70_SL_BL_LINKS_2_R56_SML_LV_RH_WERT | real | E70: Schlusslicht links 2, R56: Seitenmarkierungsleuchte links vorne, rechts hinten Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_E70_SL_BL_RECHTS_2_R56_SML_RV_LH_WERT | real | E70: Schlusslicht rechts 2, R56: Seitenmarkierungsleuchte rechts vorne, links hinten Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_KZL_WERT | real | Kennzeichenlicht Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_IBL_WERT | real | Innenbeleuchtung Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSL_LINKS_WERT | real | Nebelschlusslicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSL_RECHTS_WERT | real | Nebelschlusslicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_RFL_LINKS_WERT | real | Rueckfahrlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_RFL_RECHTS_WERT | real | Rueckfahrlicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BFD_LINKS_WERT | real | Break-Force-Display links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BFD_RECHTS_WERT | real | Break-Force-Display rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_DRL_LINKS_WERT | real | Beleuchtung WBL-Taster Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_DRL_RECHTS_WERT | real | LED Fahrtlichtkontrolle Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_KL58G_WERT | real | LED Vorfeldbeleuchtung Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_E70_SML_LINKS_VORN_R56_CS_ORANGE_WERT | real | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_E70_SML_RECHTS_VORN_R56_CS_BLAU_WERT | real | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_DIMMWERT_EINH | string | Einheit fuer Dimmwert |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-digital"></a>
### STATUS_LAMPEN_DIGITAL

KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der digitalen Stati (EIN/AUS) aller Lampen $01-&gt;RCS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_EIN | int | Fernlicht links |
| STAT_AUSGANG_FL_RECHTS_EIN | int | Fernlicht rechts |
| STAT_AUSGANG_AL_LINKS_EIN | int | Abblendlicht links |
| STAT_AUSGANG_AL_RECHTS_EIN | int | Abblendlicht rechts |
| STAT_AUSGANG_BEGRL_LINKS_EIN | int | Begrenzungslicht links |
| STAT_AUSGANG_BEGRL_RECHTS_EIN | int | Begrenzungslicht rechts |
| STAT_AUSGANG_NSW_LINKS_EIN | int | Nebelscheinwerfer links |
| STAT_AUSGANG_NSW_RECHTS_EIN | int | Nebelscheinwerfer rechts |
| STAT_AUSGANG_FRA_LINKS_VORN_EIN | int | Fahrtrichtungsanzeiger links vorne |
| STAT_AUSGANG_FRA_RECHTS_VORN_EIN | int | Fahrtrichtungsanzeiger rechts vorne |
| STAT_AUSGANG_FRA_LINKS_HINTEN_EIN | int | Fahrtrichtungsanzeiger links hinten |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_EIN | int | Fahrtrichtungsanzeiger rechts hinten |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int | Bremslicht links |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int | Bremslicht mitte |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int | Bremslicht rechts |
| STAT_AUSGANG_SL_BL_LINKS_1_EIN | int | Schlusslicht links 1 |
| STAT_AUSGANG_SL_BL_RECHTS_1_EIN | int | Schlusslicht rechts 1 |
| STAT_AUSGANG_E70_SL_BL_LINKS_2_R56_SML_LV_RH_EIN | int | E70: Schlusslicht links 2, R56: Seitenmarkierungsleuchte links vorne, rechts hinten |
| STAT_AUSGANG_E70_SL_BL_RECHTS_2_R56_SML_RV_LH_EIN | int | E70: Schlusslicht rechts 2, R56: Seitenmarkierungsleuchte rechts vorne, links hinten |
| STAT_AUSGANG_KZL_EIN | int | Kennzeichenlicht |
| STAT_AUSGANG_IBL_EIN | int | Innenbeleuchtung |
| STAT_AUSGANG_NSL_LINKS_EIN | int | Nebelschlusslicht links |
| STAT_AUSGANG_NSL_RECHTS_EIN | int | Nebelschlusslicht rechts |
| STAT_AUSGANG_RFL_LINKS_EIN | int | Rueckfahrlicht links |
| STAT_AUSGANG_RFL_RECHTS_EIN | int | Rueckfahrlicht rechts |
| STAT_AUSGANG_BFD_LINKS_EIN | int | Break-Force-Display links |
| STAT_AUSGANG_BFD_RECHTS_EIN | int | Break-Force-Display rechts |
| STAT_AUSGANG_DRL_LINKS_EIN | int | Tagfahrlicht links |
| STAT_AUSGANG_DRL_RECHTS_EIN | int | Tagfahrlicht rechts |
| STAT_AUSGANG_KL58G_EIN | int | Klemme 58G |
| STAT_AUSGANG_E70_SML_LINKS_VORN_R56_CS_ORANGE_EIN | int | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange |
| STAT_AUSGANG_E70_SML_RECHTS_VORN_R56_CS_BLAU_EIN | int | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-lesen"></a>
### STATUS_SENSE_LESEN

Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $17 Sensewert Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Auswahl, welche Lampe geprueft werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAMPE | string | ausgewaehlte Lampe |
| STAT_SENSE_WERT_EIN_1 | unsigned char | Sensewert bei eingeschalteter Lampe |
| STAT_SENSE_WERT_EIN_2 | unsigned char | Sensewert bei eingeschalteter Lampe |
| STAT_SENSE_WERT_EIN_3 | unsigned char | Sensewert bei eingeschalteter Lampe |
| STAT_SENSE_WERT_AUS_1 | unsigned char | Sensewert bei ausgeschalteter Lampe wird momentan nicht verwendet |
| STAT_SENSE_WERT_AUS_2 | unsigned char | Sensewert bei ausgeschalteter Lampe wird momentan nicht verwendet |
| STAT_SENSE_WERT_AUS_3 | unsigned char | Sensewert bei ausgeschalteter Lampe wird momentan nicht verwendet |
| STAT_SENSE_WERT_BEREICH | unsigned char | gibt an, ob Sensewert fuer unteren Bereich = 0 oder fuer oberen Bereich = 1 aktiv ist |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-innenbeleuchtung-daueraus"></a>
### STATUS_INNENBELEUCHTUNG_DAUERAUS

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $26 Innenbeleuchtung Daueraus Auslesen, ob Innenlicht daueraus geschaltet wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INNENBELEUCHTUNG_DAUERAUS | int | Innenlicht daueraus geschaltet |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-defekte"></a>
### STATUS_LAMPEN_DEFEKTE

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $27 Lampenfehler auslesen Status Defektbits (explizit) von FRM-II lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_DEFEKTE | int | Fernlicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FL_RECHTS_DEFEKTE | int | Fernlicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_AL_LINKS_DEFEKTE | int | Abblendlicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_AL_RECHTS_DEFEKTE | int | Abblendlicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BEGRL_LINKS_DEFEKTE | int | Begrenzungslicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BEGRL_RECHTS_DEFEKTE | int | Begrenzungslicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSW_LINKS_DEFEKTE | int | Nebelscheinwerfer links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSW_RECHTS_DEFEKTE | int | Nebelscheinwerfer rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_LINKS_VORN_DEFEKTE | int | Fahrtrichtungsanzeiger links vorne table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_RECHTS_VORN_DEFEKTE | int | Fahrtrichtungsanzeiger rechts vorne table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_LINKS_HINTEN_DEFEKTE | int | Fahrtrichtungsanzeiger links hinten table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_DEFEKTE | int | Fahrtrichtungsanzeiger rechts hinten table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BREMSLICHT_LINKS_DEFEKTE | int | Bremslicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BREMSLICHT_MITTE_DEFEKTE | int | Bremslicht mitte table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BREMSLICHT_RECHTS_DEFEKTE | int | Bremslicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_SL_BL_LINKS_1_DEFEKTE | int | Schlusslicht links 1 table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_SL_BL_RECHTS_1_DEFEKTE | int | Schlusslicht rechts 1 table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_E70_SL_BL_LINKS_2_R56_SML_LV_RH_DEFEKTE | int | E70: Schlusslicht links 2, R56: Seitenmarkierungsleuchte links vorne, rechts hinten table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_E70_SL_BL_RECHTS_2_R56_SML_RV_LH_DEFEKTE | int | E70: Schlusslicht rechts 2, R56: Seitenmarkierungsleuchte rechts vorne, links hinten table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_KZL_DEFEKTE | int | Kennzeichenlicht table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_IBL_DEFEKTE | int | Innenbeleuchtung table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSL_LINKS_DEFEKTE | int | Nebelschlusslicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSL_RECHTS_DEFEKTE | int | Nebelschlusslicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_RFL_LINKS_DEFEKTE | int | Rueckfahrlicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_RFL_RECHTS_DEFEKTE | int | Rueckfahrlicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BFD_LINKS_DEFEKTE | int | Break-Force-Display links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BFD_RECHTS_DEFEKTE | int | Break-Force-Display rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_DRL_LINKS_DEFEKTE | int | Beleuchtung WBL-Taster table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_DRL_RECHTS_DEFEKTE | int | LED Fahrtlichtkontrolle table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_KL58G_DEFEKTE | int | Klemme 58G table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_E70_SML_LINKS_VORN_R56_CS_ORANGE_DEFEKTE | int | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_E70_SML_RECHTS_VORN_R56_CS_BLAU_DEFEKTE | int | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flc-fla-ahl"></a>
### STATUS_FLC_FLA_AHL

Auslesen spezieller Stati KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $28 Stati fuer FLC, FLA und AHL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FLC_AKTIV | int | Licht ist ueber Status Fahrlicht eingeschaltet |
| STAT_FLA_AKTIV | int | Fernlichtassistent ist aktiv |
| STAT_FL_WEGEN_FLA_AKTIV | int | Fernlicht (BiXenon) aufgrund von Fernlichtassistent ist aktiv |
| STAT_AHL_AKTIV | int | AHL ist aktiv, d.h. Auswirkung von Lenkwinkel und Gierrate |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeugneigung"></a>
### STATUS_FAHRZEUGNEIGUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $30 STATUS_FAHRZEUGNEIGUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FAHRZEUGNEIGUNG | real | Fahrzeugneigung auslesen |
| STAT_FAHRZEUGNEIGUNG_EINH | string | Einheit fuer Fahrzeugneigung [Grad] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kindersicherung"></a>
### STATUS_KINDERSICHERUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0D Kindersicherung Status von FRMFA lesen Status der Kindersicherung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_KINDERSICHERUNG_EIN | int | Taster fuer Kindersicherung betaetigt |
| STAT_KINDERSICHERUNG_AKTIV | int | Kindersicherung ein/aus |
| STAT_KINDERSICHERUNG_EIN | string | Kindersicherung ein/aus |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dimmwert-led"></a>
### STATUS_DIMMWERT_LED

KWP2000: $30-&gt;IOCBLI $35-&gt;Auslesen der digitalen Stati (%) aller Lampen $01-&gt;RCS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FLC_LED_WERT | real | FLC LED Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_WHF_LED_WERT | real | Warning Lights switch LED Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_ILUM_PFIE_LED_WERT | real | Prefield LED ilumination Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_DIMMWERT_EINH | string | Einheit fuer Dimmwert |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-led-digital"></a>
### STATUS_LED_DIGITAL

KWP2000: $30-&gt;IOCBLI $35-&gt;Auslesen der digitalen Stati (EIN/AUS) aller LED $01-&gt;RCS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FLC_LED_EIN | int | FLC LED |
| STAT_AUSGANG_WHF_LED_EIN | int | Warning Lights switch LED |
| STAT_AUSGANG_ILUM_PFIE_LED_EIN | int | Prefield LED ilumination |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bixenon-klappe"></a>
### STATUS_BIXENON_KLAPPE

KWP2000: $30-&gt;IOCBLI $36-&gt;Auslesen der digitalen Stati (EIN/AUS) aller LED $01-&gt;RCS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_BIXENON_KLAPPE_EIN | int | BI-Xenon Klappe ausgang |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-warnblinken"></a>
### STATUS_WARNBLINKEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 Warnblinken Status von FRM-II lesen Status ob Warnblinken aktiv ist auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WARNBLINKEN_EIN | string | Warnblinken aktiv |
| STAT_WARNBLINKEN_WERT_EIN | int | Warnblinken aktiv 1 bzw. 0 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-comicro-lear"></a>
### _FLASH_COMICRO_LEAR

Flashen des CoMicro mit Daten aus dem Flash KWP2000: $2E WriteDataByCommonIdentifier $0001 Flash CoMicro

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-variable-co-micro-lear"></a>
### _READ_VARIABLE_CO_MICRO_LEAR

Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $07 Variable Co-Micro

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VAR_CO_MICRO | binary | Variablen Co-Micro |
| WATCHDOG1 | int | Variablen Co-Micro |
| WATCHDOG1_MAX | int | Variablen Co-Micro |
| WATCHDOG2 | int | Variablen Co-Micro |
| WATCHDOG2_MAX | int | Variablen Co-Micro |
| NO_OF_COMMANDS | int | Variablen Co-Micro |
| SPI_MISMATCHES | int | Variablen Co-Micro |
| NOTLAUF_COUNTER | int | Variablen Co-Micro |
| MICRO_PORT_B | int | Variablen Co-Micro |
| MICRO_PORT_C | int | Variablen Co-Micro |
| MICRO_PORT_D | int | Variablen Co-Micro |
| WAKEUP_PORT_B | int | Variablen Co-Micro |
| WAKEUP_PORT_C | int | Variablen Co-Micro |
| WAKEUP_PORT_D | int | Variablen Co-Micro |
| VOR_SLEEP_PORT_B | int | Variablen Co-Micro |
| VOR_SLEEP_PORT_C | int | Variablen Co-Micro |
| VOR_SLEEP_PORT_D | int | Variablen Co-Micro |
| WAKE_UP_1 | int | Variablen Co-Micro |
| WAKE_UP_2 | int | Variablen Co-Micro |
| RESERVE_1 | int | Variablen Co-Micro |
| POLL_TIME_SNU | int | Variablen Co-Micro |
| POLL_TIME_TK | int | Variablen Co-Micro |
| SCLOSS_COUNTER | int | Variablen Co-Micro |
| OFFSET_ADC6 | int | Variablen Co-Micro |
| OFFSET_ADC7 | int | Variablen Co-Micro |
| WERT_ADC0 | int | Variablen Co-Micro |
| WERT_ADC1 | int | Variablen Co-Micro |
| WERT_ADC2 | int | Variablen Co-Micro |
| WERT_ADC3 | int | Variablen Co-Micro |
| WERT_ADC4 | int | Variablen Co-Micro |
| WERT_ADC5 | int | Variablen Co-Micro |
| WERT_ADC6 | int | Variablen Co-Micro |
| WERT_ADC7 | int | Variablen Co-Micro |
| SLEEPTIME_0 | int | Variablen Co-Micro |
| SLEEPTIME_1 | int | Variablen Co-Micro |
| SLEEPTIME_2 | int | Variablen Co-Micro |
| SLEEPTIME_3 | int | Variablen Co-Micro |
| SLEEP_TIME | int | Variablen Co-Micro |
| RESERVE_2 | int | Variablen Co-Micro |
| PWM | int | Variablen Co-Micro |
| STATE_WBL | int | Variablen Co-Micro |
| CONFIG_FLAGS | int | Variablen Co-Micro |
| NOT_BL_FLAGS | int | Variablen Co-Micro |
| NOT_SL_FLAGS | int | Variablen Co-Micro |
| RESERVE_3 | int | Variablen Co-Micro |
| VERSION | int | Variablen Co-Micro |
| PROJEKT_NAME | string | Variablen Co-Micro |
| LINK_DATUM | string | Variablen Co-Micro |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-comicro-wd"></a>
### _STEUERN_RESET_COMICRO_WD

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1C Reset comicro WatchDog Steuern von FRM II schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hw-notlauf"></a>
### STEUERN_HW_NOTLAUF

Loeschen des CoMicro KWP2000: $3B WriteDataByLocalIdentifier $07 Co-Micro

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HW_NOTLAUF | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-erase-comicro-lear"></a>
### _ERASE_COMICRO_LEAR

Loeschen des CoMicro KWP2000: $3B WriteDataByLocalIdentifier $07 Co-Micro

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-block-lesen-lear"></a>
### _CODIERDATEN_BLOCK_LESEN_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Bereich: 0x30xx bis 0x35xx |

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

<a id="job-codierdaten-3400-lesen-komplett-lear"></a>
### _CODIERDATEN_3400_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3400-Bereich Auslesen der FRMFA-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_FRMFA | string | die kompletten Codierdaten im 3400-Bereich (FRMFA) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3500-lesen-komplett-lear"></a>
### _CODIERDATEN_3500_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3500-Bereich (FH) KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_FH | string | die kompletten Codierdaten im 3500-Bereich |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3000-lesen-komplett-lear"></a>
### _CODIERDATEN_3000_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3000-Bereich Auslesen der ALC-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_ALC | string | die kompletten Codierdaten im 3000-Bereich (ALC) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3400-schreiben-aus-datei-lear"></a>
### _CODIERDATEN_3400_SCHREIBEN_AUS_DATEI_LEAR

Beschreiben der Default-Codierdaten Beschreiben der FRMFA-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $34xx Codierdaten, Default Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten fuer 3400-Bereich Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-komplett-schreiben-lear"></a>
### _CODIERDATEN_KOMPLETT_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten AHL schreiben $31xx Codierdaten Code schreiben $32xx Codierdaten SMC_L schreiben $33xx Codierdaten SMC_R schreiben $34xx Codierdaten FRMFA schreiben $35xx Codierdaten FH schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-i-stufe-lesen-lear"></a>
### _I_STUFE_LESEN_LEAR

Auslesen der I-Stufe KWP2000: $22 ReadDataByCommonIdentifier $100B I-Step Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| I_STEP_1 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_2 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_3 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-i-stufe-schreiben-lear"></a>
### _I_STUFE_SCHREIBEN_LEAR

Beschreiben der I-Stufe Es muessen immer alle drei Argumente im Bereich von 0-65535 bzw. 0x0000-0xFFFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $100B I-Step Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_STEP_1 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_2 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_3 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-fvin"></a>
### READ_FVIN

liest die lange Fahrgestellnummer KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FVIN | string | lange Fahrgestellnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-fvin"></a>
### WRITE_FVIN

schreibt die lange Fahrgestellnummer KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FVIN | string | lange Fahrgestellnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fvin-auftrag"></a>
### FVIN_AUFTRAG

lange Fahrgestellnummer schreiben und ruecklesen KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FVIN | string | lange Fahrgestellnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-brif-schreiben-lear"></a>
### _BRIF_SCHREIBEN_LEAR

Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HWREF | string | Hardware Reference Length is 7 Default value is '009FRM0' |
| PECUHN | string | Physical ECU Hardware Number Format is XX XX XX XX XX XX (6 bytes length) Default value is '00 00 01 23 45 67' |
| DOECUM | string | Date of ECU Manufacturing Format either DD.MM.YYYY or YYMMDD Default value is 15.10.2004 |
| SSI | unsigned char | System Supplier Index Range is 0x00-0xFE Default value is 09 |
| SSECUSN | string | System Supplier ECU Serial Number Length is 9 Default value is '000000001' |
| ERT | unsigned char | Erase Time Range is 0x00-0xFE Default value is 0x10 |
| SIGT | unsigned char | Signature Time Range is 0x00-0xFE Default value is 0x20 |
| RST | unsigned char | Reset Time Range is 0x00-0xFE Default value is 0x02 |
| MXBL | unsigned char | Max block length Range is 0x00-0xFE Default value is 0xF1 |
| VMECUHVN | unsigned char | Vehicle Manufacturer ECU Version Number Range is 0x00-0xFE Default value is 0x01 |
| SNOET | string | System Name Or Engine Type Format is XX XX Default value is '41 4F' |
| ZB_NR | string | ZusBau Number Format is XX XX XX XX XX XX (6 bytes length) Default value is '00 00 01 23 45 67' |
| VAR_NR | unsigned char | Variant Number Range is 0x00-0xFE Default value is 0x01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-brif-file-lear"></a>
### _BRIF_FILE_LEAR

Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FILE_TEXT | string | Format: [Drive]:[Path]\[File].[Ext] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HWREF | string | Written Value |
| PECUHN | string | Written Value |
| DOECUM | string | Written Value |
| SSI | string | Written Value |
| SSECUSN | string | Written Value |
| ERT | string | Written Value |
| SIGT | string | Written Value |
| RST | string | Written Value |
| MXBL | string | Written Value |
| VMECUHVN | string | Written Value |
| SNOET | string | Written Value |
| UIF_ZB_NR | string | Written Value |
| VARIANT | string | Written Value |
| JOB_STATUS | string | From JobResult Table |

<a id="job-status-betr-h-funktionen"></a>
### STATUS_BETR_H_FUNKTIONEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Betriebsstunden fuer alle Funktionen Status von FRMFA lesen Lesen der Betriebsstunden der einzelnen Lampenfunktionen des FRM-II

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_FRMFA_WERT | real | Betriebsstunden FRMFA auslesen |
| STAT_BETRIEBSZEIT_FL_WERT | unsigned long | Betr_h Fernlicht |
| STAT_BETRIEBSZEIT_AL_WERT | unsigned long | Betr_h Abblendlicht |
| STAT_BETRIEBSZEIT_SL_WERT | unsigned long | Betr_h Standlicht |
| STAT_BETRIEBSZEIT_NSW_WERT | unsigned long | Betr_h Nebelscheinwerfer |
| STAT_BETRIEBSZEIT_FRA_LINKS_WERT | unsigned long | Betr_h Fahrtrichtungsanzeiger links |
| STAT_BETRIEBSZEIT_FRA_RECHTS_WERT | unsigned long | Betr_h Fahrtrichtungsanzeiger rechts |
| STAT_BETRIEBSZEIT_BL_WERT | unsigned long | Betr_h Bremslicht |
| STAT_BETRIEBSZEIT_BFD_WERT | unsigned long | Betr_h Break-Force-Display |
| STAT_BETRIEBSZEIT_NSL_WERT | unsigned long | Betr_h Nebelschlusslicht |
| STAT_BETRIEBSZEIT_RFL_WERT | unsigned long | Betr_h Rueckfahrlicht |
| STAT_BETRIEBSZEIT_IB_WERT | unsigned long | Betr_h Innenbeleuchtung |
| STAT_BETRIEBSZEIT_PL_WERT | unsigned long | Betr_h Parklicht |
| STAT_BETRIEBSZEIT_FH_L_WERT | unsigned long | Betr_h Fensterheber links |
| STAT_BETRIEBSZEIT_FH_R_WERT | unsigned long | Betr_h Fensterheber rechts |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebsstunden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-loeschen"></a>
### STEUERN_BETR_H_LOESCHEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Betriebsstunden Status von FRMFA schreiben Loeschen aller Betriebsstunden des FRM-II

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schlossnuesse"></a>
### STATUS_SCHLOSSNUESSE

Auslesen der Stati von den Schlossnuessen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Schlossnuesse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTNUSS_STELLUNG_NULL_EIN | int | Schaltnuesse in Stellung Neutral |
| STAT_SCHALTNUSS_STELLUNG_ENTRIEGELN_EIN | int | Schaltnuesse in Stellung Entriegeln |
| STAT_SCHALTNUSS_STELLUNG_SICHERN_EIN | int | Schaltnuesse in Stellung Sichern |
| STAT_SCHALTNUSS_STELLUNG_UNGUELTIG_EIN | int | Schaltnuesse in Stellung Ungueltig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lwr-position"></a>
### STATUS_LWR_POSITION

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $09 STATUS_LWR_POSITION

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LWR_POSITION_GRAD | int | Position der Schrittmotoren anzusteuernd in 1/100 Grad |
| STAT_LWR_POSITION | int | Position der Schrittmotoren tatsaechlich je nach Scheinwerfer max. von 0 bis 1000 Halbschritte der Arbeitspunkt haengt von Fahrzeugtyp und Scheinwerfer ab und ist kodierbar |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-xenon-al-einschaltversuche"></a>
### STATUS_XENON_AL_EINSCHALTVERSUCHE

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $14 Xenon-AL-Einschaltversuche Auslesen wie oft das Abblendlicht eingeschaltet wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_XENON_AL_EINSCHALTVERSUCHE | int | Xenon-AL-Einschaltversuche auslesen |
| STAT_XENON_AL_L_RESTART_VERSUCHE | int | Xenon-AL-Einschaltrestartversuche links auslesen |
| STAT_XENON_AL_R_RESTART_VERSUCHE | int | Xenon-AL-Einschaltrestartversuche rechts auslesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-xenon-al-einschaltversuche-loeschen"></a>
### STEUERN_XENON_AL_EINSCHALTVERSUCHE_LOESCHEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $14 Xenon-AL-Einschaltversuche Loeschen der AL-Einschaltversuche

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hoehenstand"></a>
### STATUS_HOEHENSTAND

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $33 STATUS_HOEHENSTAND Auslesen der Hoehenstandswerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HOEHENSTANDSSENSOR_VORNE | real | Hoehenstandssensor vorne auslesen |
| STAT_HOEHENSTANDSSENSOR_HINTEN | real | Hoehenstandssensor hinten auslesen |
| STAT_HOEHENSTANDSSENSOR_EINHEIT | string | Einheit fuer die Hoehenstandssensoren Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-wartezeit-lear"></a>
### _WARTEZEIT_LEAR

Wartezeit

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WARTEZEIT | unsigned char | Wartezeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-fensterheber"></a>
### STATUS_FENSTERHEBER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0A Stati der Fensterheber fuer FRMFA Status vom FRMFA lesen Stati der einzelnen FH-Funktionen auslesen

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
| STAT_FA_FH_POSITION_WERT | int | Position Fensterheber Fahrer, nur bei eingelerntem FH |
| STAT_BF_FH_POSITION_WERT | int | Position Fensterheber Beifahrer, nur bei eingelerntem FH |
| STAT_FA_FH_CUT_OUT_EIN | int | Fensterheber Fahrer CUT_OUT |
| STAT_BF_FH_CUT_OUT_EIN | int | Fensterheber Beifahrer CUT_OUT |
| STAT_FA_FH_THERMO_SCHUTZ_STUFE_1_EIN | int | Fensterheber Fahrer THERMO_SCHUTZ_STUFE_1 nur noch Heben des Fahrerfensters moeglich |
| STAT_BF_FH_THERMO_SCHUTZ_STUFE_1_EIN | int | Fensterheber Beifahrer THERMO_SCHUTZ_STUFE_1 nur noch Heben des Beifahrerfensters moeglich |
| STAT_FA_FH_THERMO_SCHUTZ_STUFE_2_EIN | int | Fensterheber Fahrer THERMO_SCHUTZ_STUFE_2 keine Ansteuerung des Fahrerfensters mehr moeglich |
| STAT_BF_FH_THERMO_SCHUTZ_STUFE_2_EIN | int | Fensterheber Beifahrer THERMO_SCHUTZ_STUFE_2 keine Ansteuerung des Beifahrerfensters mehr moeglich |
| STAT_FA_FH_HALL_1_DEFEKT_EIN | int | Fensterheber Fahrer Hall 1 defekt |
| STAT_BF_FH_HALL_1_DEFEKT_EIN | int | Fensterheber Beifahrer Hall 1 defekt |
| STAT_FA_FH_HALL_2_DEFEKT_EIN | int | Fensterheber Fahrer Hall 2 defekt |
| STAT_BF_FH_HALL_2_DEFEKT_EIN | int | Fensterheber Beifahrer Hall 2 defekt |
| STAT_FA_FH_RELAIS_1_DEFEKT_EIN | int | 0: - 1: Fensterheber Fahrerseite Relais 1 Defekt |
| STAT_BF_FH_RELAIS_1_DEFEKT_EIN | int | 0: - 1: Fensterheber Beifahrerseite Relais 1 Defekt |
| STAT_FA_FH_RELAIS_2_DEFEKT_EIN | int | 0: - 1: Fensterheber Fahrerseite Relais 2 Defekt |
| STAT_BF_FH_RELAIS_2_DEFEKT_EIN | int | 0: - 1: Fensterheber Beifahrerseite Relais 2 Defekt |
| STAT_FA_FH_EE_CHECKSUM_ERROR_EIN | int | 0: - 1: Fensterheber Fahrerseite E² Spiegel Checksummen Fehler |
| STAT_BF_FH_EE_CHECKSUM_ERROR_EIN | int | 0: - 1: Fensterheber Beifahrerseite E² Spiegel Checksummen Fehler |
| STAT_FA_FH_DRIVE_COUNT_AFTER_INIT_WERT | int | Zaehler nach Init Fensterheber Fahrer |
| STAT_BF_FH_DRIVE_COUNT_AFTER_INIT_WERT | int | Zaehler nach Init Fensterheber Beifahrer |
| STAT_FA_FH_STROKE_TIME_WERT | int | STROKE_TIME Fensterheber Fahrer |
| STAT_BF_FH_STROKE_TIME_WERT | int | STROKE_TIME Fensterheber Beifahrer |
| STAT_FA_FH_HUBLAENGE_WERT | int | HUBLAENGE Fensterheber Fahrer |
| STAT_BF_FH_HUBLAENGE_WERT | int | HUBLAENGE Fensterheber Beifahrer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ee-fh-log-data"></a>
### STATUS_EE_FH_LOG_DATA

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EE_FH_LOG_DATA | binary | Lesen von EE_FH_LOG_DATA |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ee-fh-log-data"></a>
### STEUERN_EE_FH_LOG_DATA

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $13 EE_FH_LOG_DATA Status von FRMFA schreiben Loeschen von EE_FH_LOG_DATA des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-denormierungs-logger-lesen-lear"></a>
### _STATUS_FH_DENORMIERUNGS_LOGGER_LESEN_LEAR

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA

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

<a id="job-steuern-diagnose-brose-fh-1"></a>
### _STEUERN_DIAGNOSE_BROSE_FH_1

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1B Diagnose fuer BROSE-FH $01 job 1 Status von FRM-II schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BROSE_DATEN_1 | string | Diagnosedaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-echtzeitdaten-brose-lesen"></a>
### _ECHTZEITDATEN_BROSE_LESEN

Echtzeitdaten vom Brose auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $18 ECHTZEITDATEN_BROSE_LESEN $01 ReportCurrentState

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

<a id="job-read-eks-supplier"></a>
### READ_EKS_SUPPLIER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $32 EKS HERSTELLER und VERSION

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAT_EKS_HERSTELLER | string | Manufacturer of the FAT EKS Table EKS_HERSTELLER Text |
| FAT_SW_VERSION | string | Software version of the FAT EKS |
| FAT_PA_VERSION | int | Coding version of the FAT EKS |
| BFT_EKS_HERSTELLER | string | Manufacturer of the BFT EKS Table EKS_HERSTELLER Text |
| BFT_SW_VERSION | string | Software version of the BFT EKS |
| BFT_PA_VERSION | int | Coding version of the BFT EKS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-denormierer"></a>
### STATUS_FH_LOGGER_DENORMIERER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DENORMIERUNGS_COUNTER | unsigned int | (Brose)Daten von SG Denormierungscounter bis 65535, danach wird nur noch auf Datensatznummer '5' gespeichert |
| STAT_DATENSATZ_1 | string | (Brose)Datensatznummer letzter abgespeicherter Datensatz |
| STAT_FEHLERNUMMER_1 | int | (Brose)Fehlernummer des Denormierers |
| STAT_FEHLERNUMMER_TEXT_1 | string | (Brose)Fehlertext des Denormierers |
| STAT_HEADER_1 | int | (Brose)Detailinformation zum Fehler |
| STAT_HEADER_TEXT_1 | string | (Brose)Text zur Detailinformation |
| STAT_POSITION_HZ_1 | int | (Brose)Scheibenposition in Hallimpulsen |
| STAT_VOLTAGE_WERT_1 | int | (Brose)Spannung am Fensterheber in Volt |
| STAT_FEHLERFLAGS_1 | int | (Brose)Fehlerdigitalstati Block 1 |
| STAT_FEHLERFLAGS_TEXT_1 | string | (Brose)Fehlerstati Block 1 als Text |
| STAT_HALLFLAGS_1 | int | (Brose)Fehlerdigitalstati Block 2 |
| STAT_HALLFLAGS_TEXT_1 | string | (Brose)Fehlerstati Block 2 als Text |
| STAT_DATENSATZ_2 | string | Datensatznummer (Brose)vorletzter abgespeicherter Datensatz |
| STAT_FEHLERNUMMER_2 | int | (Brose)Fehlernummer des Denormierers |
| STAT_FEHLERNUMMER_TEXT_2 | string | (Brose)Fehlertext des Denormierers |
| STAT_HEADER_2 | int | (Brose)Detailinformation zum Fehler |
| STAT_HEADER_TEXT_2 | string | (Brose)Text zur Detailinformation |
| STAT_POSITION_HZ_2 | int | (Brose)Scheibenposition in Hallimpulsen |
| STAT_VOLTAGE_WERT_2 | int | (Brose)Spannung am Fensterheber in Volt |
| STAT_FEHLERFLAGS_2 | int | (Brose)Fehlerdigitalstati Block 1 |
| STAT_FEHLERFLAGS_TEXT_2 | string | (Brose)Fehlerstati Block 1 als Text |
| STAT_HALLFLAGS_2 | int | (Brose)Fehlerdigitalstati Block 2 |
| STAT_HALLFLAGS_TEXT_2 | string | (Brose)Fehlerstati Block 2 als Text |
| STAT_DATENSATZ_3 | string | Datensatznummer (Brose)drittletzter abgespeicherter Datensatz |
| STAT_FEHLERNUMMER_3 | int | (Brose)Fehlernummer des Denormierers |
| STAT_FEHLERNUMMER_TEXT_3 | string | (Brose)Fehlertext des Denormierers |
| STAT_HEADER_3 | int | (Brose)Detailinformation zum Fehler |
| STAT_HEADER_TEXT_3 | string | (Brose)Text zur Detailinformation |
| STAT_POSITION_HZ_3 | int | (Brose)Scheibenposition in Hallimpulsen |
| STAT_VOLTAGE_WERT_3 | int | (Brose)Spannung am Fensterheber in Volt |
| STAT_FEHLERFLAGS_3 | int | (Brose)Fehlerdigitalstati Block 1 |
| STAT_FEHLERFLAGS_TEXT_3 | string | (Brose)Fehlerstati Block 1 als Text |
| STAT_HALLFLAGS_3 | int | (Brose)Fehlerdigitalstati Block 2 |
| STAT_HALLFLAGS_TEXT_3 | string | (Brose)Fehlerstati Block 2 als Text |
| STAT_ZEIT_WERT_1 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_1 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_1 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_1 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| STAT_ZEIT_WERT_2 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_2 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_2 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_2 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| STAT_ZEIT_WERT_3 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_3 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_3 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_3 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| STAT_ZEIT_WERT_4 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_4 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_4 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_4 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| STAT_ZEIT_WERT_5 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_5 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_5 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_5 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| STAT_ZEIT_WERT_6 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_6 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_6 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_6 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| STAT_ZEIT_WERT_7 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_7 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_7 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_7 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| STAT_ZEIT_WERT_8 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_8 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_8 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_TEXT_8 | string | (Kuester)Tabelle KUESTER_EE_DENORM_LOG |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-logger-reversierer"></a>
### STATUS_FH_LOGGER_REVERSIERER

Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $2E _STATUS_FH_REVERSIERUNGS_LOGGER_LESEN $01 ReadCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| STAT_REVERSIERUNGS_COUNTER | unsigned int | absolute Zahl der Reversierer, 0 - 65535 |
| STAT_DATENSATZ_1 | string | (Brose)Nummer des letzten Datensatzes |
| STAT_FEHLERNUMMER_1 | int | (Brose)Fehlernummer des letzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_1 | string | (Brose)Fehlertext des letzten Reversierers |
| STAT_POSITION_HZ_1 | int | (Brose)Scheibenposition in Hallsignale beim letzten Reversierer |
| STAT_VOLTAGE_WERT_1 | real | (Brose)Fensterheberspannung beim letzten Reversierer |
| STAT_AUSSENTEMP_WERT_1 | real | (Brose)Aussentemperatur in °C beim letzten Reversierer |
| STAT_SPEED_WERT_1 | real | (Brose)Fahrzeuggeschwindigkeit in km/h beim letzten Reversierer |
| STAT_DATENSATZ_2 | string | (Brose)Nummer des vorletzten Datensatzes |
| STAT_FEHLERNUMMER_2 | int | (Brose)Fehlernummer des vorletzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_2 | string | (Brose)Fehlertext des vorletzten Reversierers |
| STAT_POSITION_HZ_2 | int | (Brose)Scheibenposition in Hallsignale beim vorletzten Reversierer |
| STAT_VOLTAGE_WERT_2 | real | (Brose)Fensterheberspannung beim vorletzten Reversierer |
| STAT_AUSSENTEMP_WERT_2 | real | (Brose)Aussentemperatur in °C beim vorletzten Reversierer |
| STAT_SPEED_WERT_2 | real | (Brose)Fahrzeuggeschwindigkeit in km/h beim vorletzten Reversierer |
| STAT_DATENSATZ_3 | string | (Brose)Nummer des drittletzten Datensatzes |
| STAT_FEHLERNUMMER_3 | int | (Brose)Fehlernummer des drittletzten Reversierers |
| STAT_FEHLERNUMMER_TEXT_3 | string | (Brose)Fehlertext des drittletzten Reversierers |
| STAT_POSITION_HZ_3 | int | (Brose)Scheibenposition in Hallsignale beim drittletzten Reversierer |
| STAT_VOLTAGE_WERT_3 | real | (Brose)Fensterheberspannung beim drittletzten Reversierer |
| STAT_AUSSENTEMP_WERT_3 | real | (Brose)Aussentemperatur in °C beim drittletzten Reversierer |
| STAT_SPEED_WERT_3 | real | (Brose)Fahrzeuggeschwindigkeit in km/h beim drittletzten Reversierer |
| STAT_ZEIT_WERT_1 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_1 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_1 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_1 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_1 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_1 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_1 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| STAT_ZEIT_WERT_2 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_2 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_2 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_2 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_2 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_2 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_2 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| STAT_ZEIT_WERT_3 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_3 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_3 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_3 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_3 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_3 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_3 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| STAT_ZEIT_WERT_4 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_4 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_4 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_4 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_4 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_4 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_4 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| STAT_ZEIT_WERT_5 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_5 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_5 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_5 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_5 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_5 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_5 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| STAT_ZEIT_WERT_6 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_6 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_6 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_6 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_6 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_6 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_6 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| STAT_ZEIT_WERT_7 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_7 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_7 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_7 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_7 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_7 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_7 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| STAT_ZEIT_WERT_8 | unsigned long | (Kuester)Buszeit |
| STAT_POSITION_WERT_8 | unsigned int | (Kuester)FH position in: (mm Scheinbenweg) / 2 (Kuester)FH position in: (Scheinbenweg in Pulse) / 2.45 |
| STAT_KILOMETERSTAND_WERT_8 | unsigned int | (Kuester)Kilometerstand |
| STAT_GRUND_FH_WERT_8 | unsigned int | (Kuester)0 = FH, 1 = BFH |
| STAT_GRUND_KFZ_WERT_8 | unsigned int | (Kuester)0 = KFZ steht, 1 = KFZ faehrt |
| STAT_GRUND_SCHL_WEG_WERT_8 | unsigned int | (Kuester)0 = Schlechtweg deaktiv, 1 = Schlechtweg aktiv |
| STAT_GRUND_AUSSENTEMP_WERT_8 | real | (Kuester)Aussentemp (-30°C .. +78,5°C) |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-link-date-time-lear"></a>
### _READ_LINK_DATE_TIME_LEAR

Auslesen der Linkdate und -time KWP2000: $21 ReadDataByLocalIdentifier $01 Linkdate und -time

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_LINK_DATE_APP | string | Linkdatum fuer Applikation |
| SW_LINK_DATE_BOOT | string | Linkdatum fuer Bootloader |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-emergency-fallback-counter-lear"></a>
### _READ_EMERGENCY_FALLBACK_COUNTER_LEAR

Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $02 Fallback Counter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CME_COUNTER | int | gibt an wie oft der CME als Notlauf-Fallback zugeschlagen hat |
| CRG_PLL_LOCK_COUNTER | int | gibt an wie oft der CRG_PLL_LOCK als Notlauf-Fallback zugeschlagen hat |
| SCME_COUNTER | int | gibt an wie oft der SCME als Notlauf-Fallback zugeschlagen hat |
| ILLEGAL_OPCODE_COUNTER | int | gibt an wie oft der ILLEGAL_OPCODE als Notlauf-Fallback zugeschlagen hat |
| SWI_COUNTER | int | gibt an wie oft der SWI als Notlauf-Fallback zugeschlagen hat |
| XIRQ_COUNTER | int | gibt an wie oft der XIRQ als Notlauf-Fallback zugeschlagen hat |
| XGATE_COUNTER | int | Fehlerzaehler fuer das X-Gate |
| STACK_COUNTER | int | Fehlerzaehler fuer das Stack |
| NOTLAUF_COUNTER | int | Fehlerzaehler fuer das comicro notlauf |
| LVI_COUNTER | int | Fehlerzaehler fuer das low voltage interrupt |
| COP_COUNTER | int | Fehlerzaehler fuer das watchdog |
| ADDR_ILLEGAL_COUNTER | int | Fehlerzaehler fuer das illegal address violation |
| SPURIOUS_COUNTER | int | Fehlerzaehler fuer das spurious interrupt |
| INVALID_INT_COUNTER | int | Fehlerzaehler fuer das invalid interrupt |
| MARGINAL_READ_FLASH_COUNTER | int | Fehlerzaehler fuer das flash-rom marginal counter |
| RESET_COUNTER | int | Reset Counter |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-emergency-fallback-counter-lear"></a>
### _CLR_EMERGENCY_FALLBACK_COUNTER_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $02 NOTLAUF_FALLBACK_COUNTER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-abs-timer-lear"></a>
### _READ_ABS_TIMER_LEAR

Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $09 ABS_TIMER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ABS_TIMER | long | gibt den absoluten Laufzeittimer in Sekunden an |
| STAT_ABS_TIMER_EINH | string | Einheit fuer ABS_TIMER: Sekunden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-abs-timer-lear"></a>
### _CLR_ABS_TIMER_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $09 ABS_TIMER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecu-variante"></a>
### STATUS_ECU_VARIANTE

KWP 2000: $21 ReadDataByLocalIdentifier $03 VARIANTE Modus   : Default Auslesen der Variante des Steuergeraetes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VARIANTE_WERT | int | Variante als Wert |
| STAT_VARIANTEN_BEZEICHNUNG | string | Bezeichnung der Variante des Steuergeraetes |
| STAT_BAUREIHE_TEXT | string | Bezeichnung der Baureihe fuer das das Steuergeraet ist |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-lesen-lear"></a>
### _HERSTELLER_DATEN_LESEN_LEAR

Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $04 Herstellerdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HERSTELLERDATEN | binary | Herstellerdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-schreiben-lear"></a>
### _HERSTELLER_DATEN_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $3B WriteDataByLocalIdentifier $04 Herstellerdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lwr-lesen"></a>
### STATUS_LWR_LESEN

Unterscheidung zwischen dynamischer, automatischer und manueller LWR KWP2000: $21 ReadDataByLocalIdentifier $05 LWR lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEINE_LWR | unsigned char | 0 oder 1, ob LWR aktiv bei Kurvenlicht immer 1 |
| STAT_DYN_LWR | unsigned char | 0 oder 1, ob dynamisch LWR aktiv |
| STAT_AUT_LWR | unsigned char | 0 oder 1, ob automatische LWR aktiv |
| STAT_MAN_LWR | unsigned char | 0 oder 1, ob manuelle LWR aktiv |
| STAT_LWR_MIN | int | Kleinste Schrittmotorposition |
| STAT_LWR_MAX | int | Groesste Schrittmotorposition |
| STAT_LWR_SCHRITTE_REF_LAUF | int | Schrittanzahl fuer den Referenzlauf |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-saving-mode-lear"></a>
### _READ_ENERGY_SAVING_MODE_LEAR

Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ENERGY_SAVING_MODE | string | Ausgabe des Engery-Saving-Modes table EnergySaving NAME TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbd-zeichn-index-lesen-lear"></a>
### _CBD_ZEICHN_INDEX_LESEN_LEAR

Auslesen des Aenderungsindex aus den Codierdaten KWP2000: $21 ReadDataByLocalIdentifier $06 CBD_ZEICHN_INDEX lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CBD_ZEICHN_INDEX | string | Aenderungsindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-inputs"></a>
### STATUS_SENSE_INPUTS

Auslesen der Sensewerte der einzelnen Lampen KWP2000: $21 ReadDataByLocalIdentifier $08 Sensewerte lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSE_BERGL_L_WERT | real | Spannung Sensor Begrenzungslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_BERGL_R_WERT | real | Spannung Sensor Begrenzungslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_AL_L_WERT | real | Spannung Sensor Abblendlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_AL_R_WERT | real | Spannung Sensor Abblendlicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FL_L_WERT | real | Spannung Sensor Fernlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_FL_R_WERT | real | Spannung Sensor Fernlicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_NSW_L_WERT | real | Spannung Sensor Nebelscheinwerfer links Bereich: 0 V bis 5 V |
| STAT_SENSE_NSW_R_WERT | real | Spannung Sensor Nebelscheinwerfer rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_1_SL_L_WERT | real | Spannung Sensor Standlicht 1 links Bereich: 0 V bis 5 V |
| STAT_SENSE_1_SL_R_WERT | real | Spannung Sensor Standlicht 1 rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_E70_2_SL_L_R56_SML_LV_RH_WERT | real | Spannung Sensor E70: Standlicht 2 links, R56: Seitenmarkierungsleuchte links vorne, hinten rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_E70_2_SL_R_R56_SML_RV_LH_WERT | real | Spannung Sensor E70: Standlicht 2 rechts, R56: Seitenmarkierungsleuchte rechts vorne, hinten links Bereich: 0 V bis 5 V |
| STAT_SENSE_RFL_L_WERT | real | Spannung Sensor Rueckfahrscheinwerfer links Bereich: 0 V bis 5 V |
| STAT_SENSE_RFL_R_WERT | real | Spannung Sensor Rueckfahrscheinwerfer rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_NSL_L_WERT | real | Spannung Sensor Nebelschlusslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_NSL_R_WERT | real | Spannung Sensor Nebelschlusslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VL_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne links Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VR_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_HL_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger hinten links Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_HR_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger hinten rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_L_WERT | real | Spannung Sensor Bremslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_R_WERT | real | Spannung Sensor Bremslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_KZL_WERT | real | Spannung Sensor Kennzeichenlicht Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_M_WERT | real | Spannung Sensor Bremslicht mitte Bereich: 0 V bis 5 V |
| STAT_SENSE_BFD_L_WERT | real | Spannung Sensor BFD links Bereich: 0 V bis 5 V |
| STAT_SENSE_BFD_R_WERT | real | Spannung Sensor BFD rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_IB_WERT | real | Spannung Sensor Innenbeleuchtung Bereich: 0 V bis 5 V |
| STAT_SENSE_KL_58G_WERT | real | Spannung Sensor Klemme 58G Bereich: 0 V bis 5 V |
| STAT_SENSE_E70_SML_LV_R56_CS_ORANGE_WERT | real | Spannung Sensor E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange Bereich: 0 V bis 5 V |
| STAT_SENSE_E70_SML_RV_R56_CS_BLAU_WERT | real | Spannung Sensor E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau Bereich: 0 V bis 5 V |
| STAT_SENSE_DRL_L_WERT | real | Spannung Sensor Tagfahrlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_DRL_R_WERT | real | Spannung Sensor Tagfahrlicht rechts Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-bereiche"></a>
### STATUS_SENSE_BEREICHE

Auslesen der Sensewerte der einzelnen Lampen KWP2000: $21 ReadDataByLocalIdentifier $08 Sensewertebereiche lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSE_BERGL_L_BEREICH_WERT | int | Spannungsbereich Sensor Begrenzungslicht links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_BERGL_R_BEREICH_WERT | int | Spannungsbereich Sensor Begrenzungslicht rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_AL_L_BEREICH_WERT | int | Spannungsbereich Sensor Abblendlicht links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_AL_R_BEREICH_WERT | int | Spannungsbereich Sensor Abblendlicht rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_FL_L_BEREICH_WERT | int | Spannungsbereich Sensor Fernlicht links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_FL_R_BEREICH_WERT | int | Spannungsbereich Sensor Fernlicht rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_NSW_L_BEREICH_WERT | int | Spannungsbereich Sensor Nebelscheinwerfer links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_NSW_R_BEREICH_WERT | int | Spannungsbereich Sensor Nebelscheinwerfer rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_1_SL_L_BEREICH_WERT | int | Spannungsbereich Sensor Standlicht 1 links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_1_SL_R_BEREICH_WERT | int | Spannungsbereich Sensor Standlicht 1 rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_E70_2_SL_L_R56_SML_LV_RH_BEREICH_WERT | int | Spannungsbereich Sensor E70: Standlicht 2 links, R56: Seitenmarkierungsleuchte links vorne, rechts hinten 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_2_E70_SL_R_R56_SML_RV_LH_BEREICH_WERT | int | Spannungsbereich Sensor E70: Standlicht 2 rechts, R56: Seitenmarkierungsleuchte rechts vorne, links hinten 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_RFL_L_BEREICH_WERT | int | Spannungsbereich Sensor Rueckfahrscheinwerfer links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_RFL_R_BEREICH_WERT | int | Spannungsbereich Sensor Rueckfahrscheinwerfer rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_NSL_L_BEREICH_WERT | int | Spannungsbereich Sensor Nebelschlusslicht links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_NSL_R_BEREICH_WERT | int | Spannungsbereich Sensor Nebelschlusslicht rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_FRA_VL_BEREICH_WERT | int | Spannungsbereich Sensor Fahrtrichtungsanzeiger vorne links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_FRA_VR_BEREICH_WERT | int | Spannungsbereich Sensor Fahrtrichtungsanzeiger vorne rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_FRA_HL_BEREICH_WERT | int | Spannungsbereich Sensor Fahrtrichtungsanzeiger hinten links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_FRA_HR_BEREICH_WERT | int | Spannungsbereich Sensor Fahrtrichtungsanzeiger hinten rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_BL_L_BEREICH_WERT | int | Spannungsbereich Sensor Bremslicht links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_BL_R_BEREICH_WERT | int | Spannungsbereich Sensor Bremslicht rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_KZL_BEREICH_WERT | int | Spannungsbereich Sensor Kennzeichenlicht 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_BL_M_BEREICH_WERT | int | Spannungsbereich Sensor Bremslicht mitte 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_BFD_L_BEREICH_WERT | int | Spannungsbereich Sensor BFD links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_BFD_R_BEREICH_WERT | int | Spannungsbereich Sensor BFD rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_IB_BEREICH_WERT | int | Spannungsbereich Sensor Innenbeleuchtung 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_KL_58G_BEREICH_WERT | int | Spannungsbereich Sensor Klemme 58G 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_E70_SML_LV_R56_CS_ORANGE_BEREICH_WERT | int | Spannungsbereich Sensor E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_E70_SML_RV_R56_CS_BLAU_BEREICH_WERT | int | Spannungsbereich Sensor E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_DRL_L_BEREICH_WERT | int | Spannungsbereich Sensor Tagfahrlicht links 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| STAT_SENSE_DRL_R_BEREICH_WERT | int | Spannungsbereich Sensor Tagfahrlicht rechts 0 = unterer Spannungsbereich 1 = oberer Spannungsbereich |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pia-daten"></a>
### STATUS_PIA_DATEN

Auslesen der momentan aktuellen Piadaten KWP2000: $21 ReadDataByLocalIdentifier $0A Piadaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FOLLOW_ME_HOME_ZEIT | int | momentan eingestellte Zeit fuer Follow Me Home |
| STAT_QUITT_BLINK_ENTRIEGELN_EIN | int | Quittierungsblinken bei Entriegeln momentan |
| STAT_QUITT_BLINK_SICHERN_EIN | int | Quittierungsblinken bei Sichern momentan |
| STAT_MIND_ANZAHL_BLINKZYKLEN_BEI_TIPP | int | Mind.-Anzahl Blinkzyklen bei Tippblinken momentan |
| STAT_TAGFAHRLICHT_EIN | int | Tagfahrlicht momentan |
| STAT_ABBIEGELICHT_EIN | int | Abbiegelicht momentan |
| STAT_WELCOMELIGHT_EIN | int | Welcomelight momentan |
| STAT_FLA_EIN | int | Fernlichtassistent momentan |
| STAT_AHL_MODE | string | momentan ausgewaehlter AHL-Mode |
| STAT_FUNKSCHLUESSEL_PROFIL | int | momentan ausgewaehltes Funkschluessel-Profil |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
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

<a id="job-reset-kurzschluss-sperre"></a>
### _RESET_KURZSCHLUSS_SPERRE

Kurzschlusssperre ueber Diagnose ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Kurzschlusssperre ausschalten Status von FRM-II schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LAMP_NR | unsigned int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss"></a>
### STATUS_LAMPEN_KURZSCHLUSS

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $20 Lampenkurzschluss auslesen Status Lampenkurzschluesse (explizit) von FRM-II lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT ja/nein |
| STAT_FL_RECHTS_SHORT_CIRCUIT | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT ja/nein |
| STAT_AL_LINKS_SHORT_CIRCUIT | int | Abblendlicht links SHORT_CIRCUIT ja/nein |
| STAT_AL_RECHTS_SHORT_CIRCUIT | int | Abblendlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT | int | Begrenzungslicht links SHORT_CIRCUIT ja/nein |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT | int | Begrenzungslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_NSW_LINKS_SHORT_CIRCUIT | int | Nebelscheinwerfer links SHORT_CIRCUIT ja/nein |
| STAT_NSW_RECHTS_SHORT_CIRCUIT | int | Nebelscheinwerfer rechts SHORT_CIRCUIT ja/nein |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT ja/nein |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT ja/nein |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT ja/nein |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT | int | Bremslicht links SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT | int | Bremslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT | int | Bremslicht mitte SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT | int | Schlusslicht 1 links, E92/E93: Tagfahrlicht links SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT | int | Schlusslicht 1 rechts, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_E70_SL_BL_LINKS_2_R56_SML_VL_HR_SHORT_CIRCUIT | int | E70: Schlusslicht 2 links, R56: Seitenmarkierungsleuchte links vorne, hinten rechts SHORT_CIRCUIT ja/nein |
| STAT_E70_SL_BL_RECHTS_2_R56_SML_VR_HL_SHORT_CIRCUIT | int | E70: Schlusslicht 2 rechts, R56: Seitenmarkierungsleuchte rechts vorne, hinten links SHORT_CIRCUIT ja/nein |
| STAT_KZL_SHORT_CIRCUIT | int | Kennzeichenlicht SHORT_CIRCUIT ja/nein |
| STAT_IB_SHORT_CIRCUIT | int | Innenbeleuchtung SHORT_CIRCUIT ja/nein |
| STAT_NSL_LINKS_SHORT_CIRCUIT | int | Nebelschlusslicht links SHORT_CIRCUIT ja/nein |
| STAT_NSL_RECHTS_SHORT_CIRCUIT | int | Nebelschlusslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_RFL_LINKS_SHORT_CIRCUIT | int | Rueckfahrlicht links SHORT_CIRCUIT ja/nein |
| STAT_RFL_RECHTS_SHORT_CIRCUIT | int | Rueckfahrlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BFD_LINKS_SHORT_CIRCUIT | int | Brake-Force-Display links SHORT_CIRCUIT ja/nein |
| STAT_BFD_RECHTS_SHORT_CIRCUIT | int | Brake-Force-Display rechts SHORT_CIRCUIT ja/nein |
| STAT_DRL_LINKS_SHORT_CIRCUIT | int | DRL_LINKS SHORT_CIRCUIT ja/nein |
| STAT_DRL_RECHTS_SHORT_CIRCUIT | int | DRL_RECHTS SHORT_CIRCUIT ja/nein |
| STAT_E70_SML_LINKS_VORN_R56_CS_ORANGE_SHORT_CIRCUIT | int | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange SHORT_CIRCUIT ja/nein |
| STAT_E70_SML_RECHTS_VORN_R56_CS_BLAU_SHORT_CIRCUIT | int | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau SHORT_CIRCUIT ja/nein |
| STAT_KLEMME_58G_SHORT_CIRCUIT | int | Klemme 58g SHORT_CIRCUIT ja/nein |
| STAT_BIX_SHORT_CIRCUIT | int | Bi-Xenonklappe SHORT_CIRCUIT ja/nein |
| STAT_VERSORGUNG_SMCS_SHORT_CIRCUIT | int | Versorgungs SMCs SHORT_CIRCUIT ja/nein |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-wiederhol-counter"></a>
### STATUS_LAMPEN_KURZSCHLUSS_WIEDERHOL_COUNTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $21 Lampenkurzschluss Wiederholzaehler auslesen Status Lampenkurzschlusswiederholzaehler (explizit) von FRM-II lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_FL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_AL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Abblendlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_AL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Abblendlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Begrenzungslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Begrenzungslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSW_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelscheinwerfer links SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht mitte SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht 1 links, E92/E93: Tagfahrlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht 1 rechts, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_E70_SL_BL_LINKS_2_R56_SML_VL_HR_SHORT_CIRCUIT_WIEDERHOL | int | E70: Schlusslicht 2 links, R56: Seitenmarkierungsleuchte links vorne, hinten rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_E70_SL_BL_RECHTS_2_R56_SML_VR_HL_SHORT_CIRCUIT_WIEDERHOL | int | E70: Schlusslicht 2 rechts, R56: Seitenmarkierungsleuchte rechts vorne, hinten links SHORT_CIRCUIT_WIEDERHOL |
| STAT_KZL_SHORT_CIRCUIT_WIEDERHOL | int | Kennzeichenlicht SHORT_CIRCUIT_WIEDERHOL |
| STAT_IB_SHORT_CIRCUIT_WIEDERHOL | int | Innenbeleuchtung SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelschlusslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelschlusslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_RFL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Rueckfahrlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Rueckfahrlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BFD_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Brake-Force-Display links SHORT_CIRCUIT_WIEDERHOL |
| STAT_BFD_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Brake-Force-Display rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_DRL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | DRL_LINKS SHORT_CIRCUIT_WIEDERHOL |
| STAT_DRL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | DRL_RECHTS SHORT_CIRCUIT_WIEDERHOL |
| STAT_E70_SML_LINKS_VORN_R56_CS_ORANGE_SHORT_CIRCUIT_WIEDERHOL | int | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange SHORT_CIRCUIT_WIEDERHOL |
| STAT_E70_SML_RECHTS_VORN_R56_CS_BLAU_SHORT_CIRCUIT_WIEDERHOL | int | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau SHORT_CIRCUIT_WIEDERHOL |
| STAT_KLEMME_58G_SHORT_CIRCUIT_WIEDERHOL | int | Klemme 58g SHORT_CIRCUIT_WIEDERHOL |
| STAT_BIX_SHORT_CIRCUIT_WIEDERHOL | int | Bi-Xenonklappe SHORT_CIRCUIT_WIEDERHOL |
| STAT_VERSORGUNG_SMCS_SHORT_CIRCUIT_WIEDERHOL | int | Versorgung SMCs SHORT_CIRCUIT_WIEDERHOL |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-counter"></a>
### STATUS_LAMPEN_KURZSCHLUSS_COUNTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $22 Lampenkurzschluss Zaehler auslesen Status Lampenkurzschlusszaehler (explizit) von FRM-II lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_COUNTER | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT_COUNTER |
| STAT_FL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_AL_LINKS_SHORT_CIRCUIT_COUNTER | int | Abblendlicht links SHORT_CIRCUIT_COUNTER |
| STAT_AL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Abblendlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_COUNTER | int | Begrenzungslicht links SHORT_CIRCUIT_COUNTER |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Begrenzungslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_NSW_LINKS_SHORT_CIRCUIT_COUNTER | int | Nebelscheinwerfer links SHORT_CIRCUIT_COUNTER |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_COUNTER | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_COUNTER |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_COUNTER |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_COUNTER |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_COUNTER |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_COUNTER | int | Bremslicht links SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_COUNTER | int | Bremslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_COUNTER | int | Bremslicht mitte SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_COUNTER | int | Schlusslicht links 1, E92/E93: Tagfahrlicht links SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_COUNTER | int | Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_E70_SL_BL_LINKS_2_R56_SML_VL_HR_SHORT_CIRCUIT_COUNTER | int | E70: Schlusslicht 2 links, R56: Seitenmarkierungsleuchte links vorne, hinten rechts SHORT_CIRCUIT_COUNTER |
| STAT_E70_SL_BL_RECHTS_2_R56_SML_VR_HL_SHORT_CIRCUIT_COUNTER | int | E70: Schlusslicht 2 rechts, R56: Seitenmarkierungsleuchte rechts vorne, hinten links SHORT_CIRCUIT_COUNTER |
| STAT_KZL_SHORT_CIRCUIT_COUNTER | int | Kennzeichenlicht SHORT_CIRCUIT_COUNTER |
| STAT_IB_SHORT_CIRCUIT_COUNTER | int | Innenbeleuchtung SHORT_CIRCUIT_COUNTER |
| STAT_NSL_LINKS_SHORT_CIRCUIT_COUNTER | int | Nebelschlusslicht links SHORT_CIRCUIT_COUNTER |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Nebelschlusslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_RFL_LINKS_SHORT_CIRCUIT_COUNTER | int | Rueckfahrlicht links SHORT_CIRCUIT_COUNTER |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Rueckfahrlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BFD_LINKS_SHORT_CIRCUIT_COUNTER | int | Brake-Force-Display links SHORT_CIRCUIT_COUNTER |
| STAT_BFD_RECHTS_SHORT_CIRCUIT_COUNTER | int | Brake-Force-Display rechts SHORT_CIRCUIT_COUNTER |
| STAT_DRL_LINKS_SHORT_CIRCUIT_COUNTER | int | DRL_LINKS SHORT_CIRCUIT_COUNTER |
| STAT_DRL_RECHTS_SHORT_CIRCUIT_COUNTER | int | DRL_RECHTS SHORT_CIRCUIT_COUNTER |
| STAT_E70_SML_LINKS_VORN_R56_CS_ORANGE_SHORT_CIRCUIT_COUNTER | int | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange SHORT_CIRCUIT_COUNTER |
| STAT_E70_SML_RECHTS_VORN_R56_CS_BLAU_SHORT_CIRCUIT_COUNTER | int | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau SHORT_CIRCUIT_COUNTER |
| STAT_KLEMME_58G_SHORT_CIRCUIT_COUNTER | int | Klemme 58g SHORT_CIRCUIT_COUNTER |
| STAT_BIX_SHORT_CIRCUIT_COUNTER | int | Bi-Xenonklappe SHORT_CIRCUIT_COUNTER |
| STAT_VERSORGUNG_SMCS_SHORT_CIRCUIT_COUNTER | int | Versorgung SMCs SHORT_CIRCUIT_COUNTER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-counter-max"></a>
### STATUS_LAMPEN_KURZSCHLUSS_COUNTER_MAX

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $23 Lampenkurzschluss Zaehler Maxwert auslesen Status des max. Wertes des Lampenkurzschlusszaehlers (explizit) von FRM-II lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_AL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Abblendlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_AL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Abblendlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Begrenzungslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Begrenzungslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSW_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelscheinwerfer links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht mitte SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht links 1, E92/E93: Tagfahrlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_E70_SL_BL_LINKS_2_R56_SML_VL_HR_SHORT_CIRCUIT_COUNTER_MAX | int | E70: Schlusslicht 2 links, R56: Seitenmarkierungsleuchte links vorne, hinten rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_E70_SL_BL_RECHTS_2_R56_SML_VR_HL_SHORT_CIRCUIT_COUNTER_MAX | int | E70: Schlusslicht 2 rechts, R56: Seitenmarkierungsleuchte rechts vorne, hinten links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_KZL_SHORT_CIRCUIT_COUNTER_MAX | int | Kennzeichenlicht SHORT_CIRCUIT_COUNTER_MAX |
| STAT_IB_SHORT_CIRCUIT_COUNTER_MAX | int | Innenbeleuchtung SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelschlusslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelschlusslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_RFL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Rueckfahrlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Rueckfahrlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BFD_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Brake-Force-Display links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BFD_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Brake-Force-Display rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_DRL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | DRL_LINKS SHORT_CIRCUIT_COUNTER_MAX |
| STAT_DRL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | DRL_RECHTS SHORT_CIRCUIT_COUNTER_MAX |
| STAT_E70_SML_LINKS_VORN_R56_CS_ORANGE_SHORT_CIRCUIT_COUNTER_MAX | int | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange SHORT_CIRCUIT_COUNTER_MAX |
| STAT_E70_SML_RECHTS_VORN_R56_CS_BLAU_SHORT_CIRCUIT_COUNTER_MAX | int | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau SHORT_CIRCUIT_COUNTER_MAX |
| STAT_KLEMME_58G_SHORT_CIRCUIT_COUNTER_MAX | int | Klemme 58g SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BIX_SHORT_CIRCUIT_COUNTER_MAX | int | Bi-Xenonklappe SHORT_CIRCUIT_COUNTER_MAX |
| STAT_VERSORGUNG_SMCS_SHORT_CIRCUIT_COUNTER_MAX | int | Versorgung SMCs SHORT_CIRCUIT_COUNTER_MAX |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierbits"></a>
### STATUS_CODIERBITS

Auslesen spezieller Codierbits KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $26 Codierbits

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LIN_BEDIENTEIL | int | 0: kein LIN-Bedienteil codiert 1: LIN-Bedienteil codiert |
| STAT_LIN_SPIEGEL | int | 0: kein LIN-Spiegel codiert 1: LIN-Spiegel codiert |
| STAT_MEMORY_SPIEGEL | int | 0: kein Memory-Spiegel codiert 1: Memory-Spiegel codiert |
| STAT_XENON_SW | int | 0: kein Xenon codiert 1: Xenon codiert |
| STAT_ALC_SYSTEM | int | 0: kein ALC-System codiert 1: ALC-System codiert |
| STAT_GURTBRINGER | int | 0: Gurtbringer nicht codiert 1: Gurtbringer codiert |
| STAT_HOEHENSTANDSSENOREN_FCAN | int | 0: Hoehenstandssensoren ueber FCAN nicht codiert 1: Hoehenstandssensoren ueber FCAN codiert |
| STAT_FLC | int | 0: automatische Fahrlichtcontrolle nicht codiert 1: automatische Fahrlichtcontrolle codiert |
| STAT_GETRIEBE_HANDSCHALTER | int | 0: Handschalter nicht codiert 1: Handschalter codiert |
| STAT_SPIEGEL_HEIZUNG | int | 0: Spiegelheizung nicht codiert 1: Spiegelheizung codiert |
| STAT_KEINE_LWR | unsigned char | 0 oder 1, ob LWR aktiv bei Kurvenlicht immer 1 |
| STAT_DYN_LWR | unsigned char | 0 oder 1, ob dynamisch LWR aktiv |
| STAT_AUT_LWR | unsigned char | 0 oder 1, ob automatische LWR aktiv |
| STAT_MAN_LWR | unsigned char | 0 oder 1, ob manuelle LWR aktiv |
| STAT_LWR_MIN | int | Kleinste Schrittmotorposition |
| STAT_LWR_MAX | int | Groesste Schrittmotorposition |
| STAT_LWR_SCHRITTE_REF_LAUF | int | Schrittanzahl fuer den Referenzlauf |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkstock"></a>
### STATUS_LENKSTOCK

Status der Lenkstock-Funktionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LENKSTOCK_BLINKER_WERT | int | Lenkstock Blinker 0: in Nullstellung 1: Blinker links dauer betaetigt 2: Blinker links tipp betaetigt 3: Blinker rechts dauer betaetigt 4: Blinker rechts tipp betaetigt 5: Fernlicht betaetigt 6: Lichthupe betaetigt 7: Mehrfachbetaetigung Nummerierung bleibt erhalten, auch bei Entfall mehrerer Funktionen |
| STAT_LENKSTOCK_BLINKER_TEXT | string | Text zu STAT_LENKSTOCK_BLINKER_WERT siehe table STAT_LENKSTOCK_BLINKER VSWERT STATUS_TEXT |
| STAT_LENKSTOCK_BLINKER_NULLSTELLUNG | int | 0: Lenkstock Blinker nicht in Nullstellung 1: Lenkstock Blinker in Nullstellung |
| STAT_LENKSTOCK_BLINKER_RECHTS | int | 0: Lenkstock Blinker nicht in Stellung Blinker Tipp rechts 1: Lenkstock Blinker in Stellung Blinker Tipp rechts |
| STAT_LENKSTOCK_BLINKER_RECHTS_DAUER | int | 0: Lenkstock Blinker nicht in Stellung Blinker Dauer rechts 1: Lenkstock Blinker in Stellung Blinker Dauer rechts |
| STAT_LENKSTOCK_BLINKER_LINKS | int | 0: Lenkstock Blinker nicht in Stellung Blinker Tipp links 1: Lenkstock Blinker in Stellung Blinker Tipp links |
| STAT_LENKSTOCK_BLINKER_LINKS_DAUER | int | 0: Lenkstock Blinker nicht in Stellung Blinker Dauer links 1: Lenkstock Blinker in Stellung Blinker Dauer links |
| STAT_LENKSTOCK_BLINKER_FERNLICHT | int | 0: Lenkstock Blinker nicht in Stellung Fernlicht 1: Lenkstock Blinker in Stellung Fernlicht |
| STAT_LENKSTOCK_BLINKER_LICHTHUPE | int | 0: Lenkstock Blinker nicht in Stellung Lichthupe 1: Lenkstock Blinker in Stellung Lichthupe |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-ascet-input"></a>
### _STATUS_VAR_IAP_PWR_ASCET_INPUT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A Power Window Ascet Model $00 Input Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ascIN_AutomaticBFT | int |  |
| ascIN_AutomaticFAT | int |  |
| ascIN_DirectionBFT | int |  |
| ascIN_DirectionFAT | int |  |
| ascIN_DriveAckBFT | int |  |
| ascIN_DriveAckFAT | int |  |
| ascIN_DriveBFT | int |  |
| ascIN_DriveFAT | int |  |
| ascIN_FeModus | int |  |
| ascIN_KurzhubDeakt | int |  |
| ascIN_NormedBFT | int |  |
| ascIN_NormedFAT | int |  |
| ascIN_PositionBFT | int |  |
| ascIN_PositionFAT | int |  |
| ascIN_ReverseBFT | int |  |
| ascIN_ReverseFAT | int |  |
| ascIN_StKl15 | int |  |
| ascIN_StKl50 | int |  |
| ascIN_StPanMod | int |  |
| ascIN_StWrgEnb | int |  |
| ascIN_StartInitlaufBFT | int |  |
| ascIN_StartInitlaufFAT | int |  |
| ascIN_Thermo90BFT | int |  |
| ascIN_Thermo90FAT | int |  |
| ascIN_TraModus | int |  |
| ascIN_TuerOffenBFT | int |  |
| ascIN_TuerOffenFAT | int |  |
| ascIN_WeModus | int |  |
| ascOP_LtAufBFT | int |  |
| ascOP_LtAutoBFT | int |  |
| ascOP_LtZuBFT | int |  |
| ascOP_MstrAufBFT | int |  |
| ascOP_MstrAufFAT | int |  |
| ascOP_MstrAutoBFT | int |  |
| ascOP_MstrAutoFAT | int |  |
| ascOP_MstrZuBFT | int |  |
| ascOP_MstrZuFAT | int |  |
| ascOP_SztAufBFT | int |  |
| ascOP_SztAufFAT | int |  |
| ascOP_SztAutoBFT | int |  |
| ascOP_SztAutoFAT | int |  |
| ascOP_SztZuBFT | int |  |
| ascOP_SztZuFAT | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-ascet-output"></a>
### _STATUS_VAR_IAP_PWR_ASCET_OUTPUT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A Power Window Ascet Model $01 Output Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ascOUT_AnfKurzhubBFT | int |  |
| ascOUT_AnfKurzhubFAT | int |  |
| ascOUT_DenormBFT | int |  |
| ascOUT_DenormFAT | int |  |
| ascOUT_DriveBFT | int |  |
| ascOUT_DriveFAT | int |  |
| ascOUT_EksBFT | int |  |
| ascOUT_EksFAT | int |  |
| ascOUT_InitResultBFT | int |  |
| ascOUT_InitResultFAT | int |  |
| ascOUT_InitlaufBFT | int |  |
| ascOUT_InitlaufFAT | int |  |
| ascOUT_PanicBFT | int |  |
| ascOUT_PanicFAT | int |  |
| ascOUT_TargetPosBFT | int |  |
| ascOUT_TargetPosFAT | int |  |
| dT_PROJECT_FRMFA2_IMPL | long |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-ascet-cod"></a>
### _STATUS_VAR_IAP_PWR_ASCET_COD

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A Power Window Ascet Model $02 Coding Variables

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ascCOD_Coupetuer | int |  |
| ascCOD_FHMitEks | int |  |
| ascCOD_FHTippAufBFT | int |  |
| ascCOD_FHTippAufFAT | int |  |
| ascCOD_FHTippZuBFT | int |  |
| ascCOD_FHTippZuFAT | int |  |
| ascCOD_Kl50Restart | int |  |
| ascCOD_KurzhubDeaktFeWe | int |  |
| ascCOD_KurzhubdelayZu | int |  |
| ascCOD_Langhub | int |  |
| ascCOD_ManMitEks | int |  |
| ascCOD_Panikmodus | int |  |
| ascCOD_PanikmodusEks | int |  |
| ascCOD_TasterEinstufig | int |  |
| ascCOD_TueraufStopMaut | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-brose-globalvar-fat"></a>
### _STATUS_VAR_IAP_PWR_BROSE_GLOBALVAR_FAT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $00 Global Variables FAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAT_WR_DOOR | int |  |
| FAT_TCAP0V | unsigned int |  |
| FAT_TCAP1V | unsigned int |  |
| FAT_POSITION_HZ | int |  |
| FAT_POSITION_2Z | int |  |
| FAT_POSITION_4Z | int |  |
| FAT_RELAISDELAYZ | int |  |
| FAT_HALLNACHLAUFCNT | int |  |
| FAT_BLOCKSEZ | int |  |
| FAT_BLOCKHEZ | int |  |
| FAT_MOTZUSTANDV | int |  |
| FAT_POSITION_2ZALT5MS | int |  |
| FAT_MOTTIMEOUTV | unsigned int |  |
| FAT_MOTZUSTANDALTV | int |  |
| FAT_VOLTAGEV | int |  |
| FAT_TEMPVOLTAGEV | int |  |
| FAT_UNDERVOLTAGEBLINDOUTZ | int |  |
| FAT_OVERVOLTAGEBLINDOUTZ | int |  |
| FAT_VOLTAGEFLAGS | string |  |
| FAT_PERIODEV | unsigned int |  |
| FAT_ASPERIODEV | unsigned int |  |
| FAT_DCMDREHZAHLV | unsigned int |  |
| FAT_DCMASDREHZAHLV | unsigned int |  |
| FAT_ANLGEGENZ | char |  |
| FAT_POSITION_4ZALT5MS | int |  |
| FAT_REVWEG | unsigned int |  |
| FAT_ASTABV | int |  |
| FAT_NFTABV | int |  |
| FAT_ANLGLEICHZ | char |  |
| FAT_HALLERBLOCKZ | int |  |
| FAT_HALLERDREH1Z | int |  |
| FAT_HALLPOLLSI | int |  |
| FAT_HALLPOLLCO | int |  |
| FAT_RELAISENTPRELLZ | int |  |
| FAT_RKLEBZ | int |  |
| FAT_HALLERDREH2Z | int |  |
| FAT_ADOFFSETV | int |  |
| FAT_DEFICITCNT | int |  |
| FAT_CHECKTIMECNT | int |  |
| FAT_MERKNFZ | int |  |
| FAT_EEPROMsaveNewAdrOffseti | int |  |
| FAT_EEPROMsaveOldAdrOffsetk | int |  |
| FAT_HALFROTATIONS | int |  |
| FAT_DEFCNT | int |  |
| FAT_HALLUNTERABTASTCNT | int |  |
| FAT_STATEMACHINEV | int |  |
| FAT_MOTORNACHLAUFZEIT | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-brose-globalvar-bft"></a>
### _STATUS_VAR_IAP_PWR_BROSE_GLOBALVAR_BFT

Auslesen der Stati von den Internen Variablen Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $01 Global Variables BFT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BFT_WR_DOOR | int |  |
| BFT_TCAP0V | unsigned int |  |
| BFT_TCAP1V | unsigned int |  |
| BFT_POSITION_HZ | int |  |
| BFT_POSITION_2Z | int |  |
| BFT_POSITION_4Z | int |  |
| BFT_RELAISDELAYZ | int |  |
| BFT_HALLNACHLAUFCNT | int |  |
| BFT_BLOCKSEZ | int |  |
| BFT_BLOCKHEZ | int |  |
| BFT_MOTZUSTANDV | int |  |
| BFT_POSITION_2ZALT5MS | int |  |
| BFT_MOTTIMEOUTV | unsigned int |  |
| BFT_MOTZUSTANDALTV | int |  |
| BFT_VOLTAGEV | int |  |
| BFT_TEMPVOLTAGEV | int |  |
| BFT_UNDERVOLTAGEBLINDOUTZ | int |  |
| BFT_OVERVOLTAGEBLINDOUTZ | int |  |
| BFT_VOLTAGEFLAGS | string |  |
| BFT_PERIODEV | unsigned int |  |
| BFT_ASPERIODEV | unsigned int |  |
| BFT_DCMDREHZAHLV | unsigned int |  |
| BFT_DCMASDREHZAHLV | unsigned int |  |
| BFT_ANLGEGENZ | int |  |
| BFT_POSITION_4ZALT5MS | int |  |
| BFT_REVWEG | unsigned int |  |
| BFT_ASTABV | int |  |
| BFT_NFTABV | int |  |
| BFT_ANLGLEICHZ | int |  |
| BFT_HALLERBLOCKZ | int |  |
| BFT_HALLERDREH1Z | int |  |
| BFT_HALLPOLLSI | int |  |
| BFT_HALLPOLLCO | int |  |
| BFT_RELAISENTPRELLZ | int |  |
| BFT_RKLEBZ | int |  |
| BFT_HALLERDREH2Z | int |  |
| BFT_ADOFFSETV | int |  |
| BFT_DEFICITCNT | int |  |
| BFT_CHECKTIMECNT | int |  |
| BFT_MERKNFZ | int |  |
| BFT_EEPROMsaveNewAdrOffseti | int |  |
| BFT_EEPROMsaveOldAdrOffsetk | int |  |
| BFT_HALFROTATIONS | int |  |
| BFT_DEFCNT | int |  |
| BFT_HALLUNTERABTASTCNT | int |  |
| BFT_STATEMACHINEV | int |  |
| BFT_MOTORNACHLAUFZEIT | int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-brose-globalflg-fat"></a>
### _STATUS_VAR_IAP_PWR_BROSE_GLOBALFLG_FAT

Auslesen der Stati von den Internen Variablen Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $02 Global Flags FAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAT_SCHALTER1V | string |  |
| FAT_SCHALTER2V | string |  |
| FAT_SCHALTER3V | string |  |
| FAT_SCHALTER4V | string |  |
| FAT_SCHALTER5V | string |  |
| FAT_SCHALTER6V | string |  |
| FAT_SCHALTER7V | string |  |
| FAT_NormF | int |  |
| FAT_BlockHeF | int |  |
| FAT_BlockSeF | int |  |
| FAT_SeBlockNormF | int |  |
| FAT_MotStatus1F | int |  |
| FAT_MotStatus2F | int |  |
| FAT_MovementF | int |  |
| FAT_PosWriteOKF | int |  |
| FAT_Rel1F | int |  |
| FAT_Rel2F | int |  |
| FAT_revF | int |  |
| FAT_RevAltF | int |  |
| FAT_senkenF | int |  |
| FAT_hebenF | int |  |
| FAT_senkenFaltF | int |  |
| FAT_hebenFalt | int |  |
| FAT_MotFlankF | int |  |
| FAT_AutomaticF | int |  |
| FAT_NAutomaticF | int |  |
| FAT_AutomaticOldF | int |  |
| FAT_MerkNfF | int |  |
| FAT_MerkSchlagF | int |  |
| FAT_MottimeoutF | int |  |
| FAT_DenormOldF | int |  |
| FAT_VerdeckNachnormF | int |  |
| FAT_Thermo100F | int |  |
| FAT_Thermo100AltF | int |  |
| FAT_Thermo90F | int |  |
| FAT_AnlGleichF | int |  |
| FAT_AnlGegenF | int |  |
| FAT_DenormF | int |  |
| FAT_RelaisKleber1F | int |  |
| FAT_RelaisKleber2F | int |  |
| FAT_MotFlankISRF | int |  |
| FAT_HallTauschFlankeF | int |  |
| FAT_TCapEvent | int |  |
| FAT_H1H2ExorF | int |  |
| FAT_HallInterruptF | int |  |
| FAT_PositionInc | int |  |
| FAT_PositionDec | int |  |
| FAT_IrqProtect | int |  |
| FAT_HallOldF | int |  |
| FAT_HallErrMayBeF | int |  |
| FAT_HallErrMayBeOldF | int |  |
| FAT_DirDriveChangeF | int |  |
| FAT_Hall1ShotF | int |  |
| FAT_Hall2ShotF | int |  |
| FAT_Hall1ShotAltF | int |  |
| FAT_Hall2ShotAltF | int |  |
| FAT_HallErBlockF | int |  |
| FAT_HallErrorF | int |  |
| FAT_HallErDrehF | int |  |
| FAT_HallErrorISF | int |  |
| FAT_HallErrorICF | int |  |
| FAT_BlockHeMerk | int |  |
| FAT_BlockSeMerk | int |  |
| FAT_HallDirError | int |  |
| FAT_HallSpeedError | int |  |
| FAT_DirHeMerk | int |  |
| FAT_DirSeMerk | int |  |
| FAT_CheckEchtError17F | int |  |
| FAT_Checkecht16NIOF | int |  |
| FAT_Checkecht17NIOF | int |  |
| FAT_EepromCheckNIOF | int |  |
| FAT_EepromCheckNIOAltF | int |  |
| FAT_PosAF | int |  |
| FAT_PosBF | int |  |
| FAT_PosCF | int |  |
| FAT_PosDF | int |  |
| FAT_PosEF | int |  |
| FAT_PosFF | int |  |
| FAT_PosGF | int |  |
| FAT_PosB1F | int |  |
| FAT_PosCInitF | int |  |
| FAT_ROBELFLAGS | string |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-brose-globalflg-bft"></a>
### _STATUS_VAR_IAP_PWR_BROSE_GLOBALFLG_BFT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $03 Global Flags BFT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BFT_SCHALTER1V | string |  |
| BFT_SCHALTER2V | string |  |
| BFT_SCHALTER3V | string |  |
| BFT_SCHALTER4V | string |  |
| BFT_SCHALTER5V | string |  |
| BFT_SCHALTER6V | string |  |
| BFT_SCHALTER7V | string |  |
| BFT_NormF | int |  |
| BFT_BlockHeF | int |  |
| BFT_BlockSeF | int |  |
| BFT_SeBlockNormF | int |  |
| BFT_MotStatus1F | int |  |
| BFT_MotStatus2F | int |  |
| BFT_MovementF | int |  |
| BFT_PosWriteOKF | int |  |
| BFT_Rel1F | int |  |
| BFT_Rel2F | int |  |
| BFT_revF | int |  |
| BFT_RevAltF | int |  |
| BFT_senkenF | int |  |
| BFT_hebenF | int |  |
| BFT_senkenFaltF | int |  |
| BFT_hebenFalt | int |  |
| BFT_MotFlankF | int |  |
| BFT_AutomaticF | int |  |
| BFT_NAutomaticF | int |  |
| BFT_AutomaticOldF | int |  |
| BFT_MerkNfF | int |  |
| BFT_MerkSchlagF | int |  |
| BFT_MottimeoutF | int |  |
| BFT_DenormOldF | int |  |
| BFT_VerdeckNachnormF | int |  |
| BFT_Thermo100F | int |  |
| BFT_Thermo100AltF | int |  |
| BFT_Thermo90F | int |  |
| BFT_AnlGleichF | int |  |
| BFT_AnlGegenF | int |  |
| BFT_DenormF | int |  |
| BFT_RelaisKleber1F | int |  |
| BFT_RelaisKleber2F | int |  |
| BFT_MotFlankISRF | int |  |
| BFT_HallTauschFlankeF | int |  |
| BFT_TCapEvent | int |  |
| BFT_H1H2ExorF | int |  |
| BFT_HallInterruptF | int |  |
| BFT_PositionInc | int |  |
| BFT_PositionDec | int |  |
| BFT_IrqProtect | int |  |
| BFT_HallOldF | int |  |
| BFT_HallErrMayBeF | int |  |
| BFT_HallErrMayBeOldF | int |  |
| BFT_DirDriveChangeF | int |  |
| BFT_Hall1ShotF | int |  |
| BFT_Hall2ShotF | int |  |
| BFT_Hall1ShotAltF | int |  |
| BFT_Hall2ShotAltF | int |  |
| BFT_HallErBlockF | int |  |
| BFT_HallErrorF | int |  |
| BFT_HallErDrehF | int |  |
| BFT_HallErrorISF | int |  |
| BFT_HallErrorICF | int |  |
| BFT_BlockHeMerk | int |  |
| BFT_BlockSeMerk | int |  |
| BFT_HallDirError | int |  |
| BFT_HallSpeedError | int |  |
| BFT_DirHeMerk | int |  |
| BFT_DirSeMerk | int |  |
| BFT_CheckEchtError17F | int |  |
| BFT_Checkecht16NIOF | int |  |
| BFT_Checkecht17NIOF | int |  |
| BFT_EepromCheckNIOF | int |  |
| BFT_EepromCheckNIOAltF | int |  |
| BFT_PosAF | int |  |
| BFT_PosBF | int |  |
| BFT_PosCF | int |  |
| BFT_PosDF | int |  |
| BFT_PosEF | int |  |
| BFT_PosFF | int |  |
| BFT_PosGF | int |  |
| BFT_PosB1F | int |  |
| BFT_PosCInitF | int |  |
| BFT_ROBELFLAGS | string |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-brose-control-fat"></a>
### _STATUS_VAR_IAP_PWR_BROSE_CONTROL_FAT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $04 Control Variables FAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IN_FAT_ENABLE_EKS | int |  |
| IN_FAT_DIRECTION | int |  |
| IN_FAT_DRIVE | int |  |
| IN_FAT_SHORT_LIFT | int |  |
| IN_FAT_DOORAJAR | int |  |
| IN_FAT_LOCKSTATE | int |  |
| IN_FAT_OTHER_WINDOW_STATE | int |  |
| IN_FAT_PANIC_ONE | int |  |
| IN_FAT_USASTANDART | int |  |
| IN_FAT_IGNITION_KEY | int | KL_15 |
| IN_FAT_KL_50 | int | KL_50 |
| IN_FAT_FH_MOTOR_P | int |  |
| IN_FAT_FH_MOTOR_M | int |  |
| IN_FAT_INITJOB | int |  |
| IN_FAT_ENABLE_TESTEKS | int |  |
| IN_PERFORMANCE_MEASUREMENT | int |  |
| IN_FAT_AUSENTEMP | int |  |
| IN_FAT_STANDZEIT | long |  |
| IN_FAT_SPEED | int |  |
| IN_FAT_TOPSTATUS | int |  |
| IN_FAT_VOLTAGE | int |  |
| IN_FAT_STOP_POSITION | unsigned int |  |
| IN_FAT_STROKELENGTH | unsigned int |  |
| IN_FAT_FETRAWE | int |  |
| LB_FAT_DENORMIEREN | int |  |
| LB_FAT_WAKEUPF | int |  |
| LB_FAT_POWER_ONF | int |  |
| BL_FAT_EE_WRITE_Z4 | int |  |
| BL_FAT_EE_WRITE_Z5 | int |  |
| BL_FAT_EE_WRITE_Z6 | int |  |
| BL_FAT_EE_WRITE_Z7 | int |  |
| BL_FAT_EE_WRITE_DLOG | int |  |
| BL_FAT_EE_WRITE_RLOG | int |  |
| OUT_FAT_CUTOUT | int |  |
| OUT_FAT_DRIVE | int |  |
| OUT_FAT_DIRECTION | int |  |
| OUT_FAT_AUTOMATIC | int |  |
| OUT_FAT_OVERHEAT90 | int |  |
| OUT_FAT_OVERHEAT100 | int |  |
| OUT_FAT_HALLDEFECT | int |  |
| OUT_FAT_HALL1DEFECT | int |  |
| OUT_FAT_HALL2DEFECT | int |  |
| OUT_FAT_RELAIS1DEFECT | int |  |
| OUT_FAT_RELAIS1VAL | int |  |
| OUT_FAT_RELAIS2DEFECT | int |  |
| OUT_FAT_RELAIS2VAL | int |  |
| OUT_FAT_NORMSTATE | int |  |
| OUT_FAT_DEBUGMODE | int |  |
| OUT_FAT_WINDOW_OPENED_COMPLETE | int |  |
| OUT_FAT_WINDOW_CLOSED_COMPLETE | int |  |
| OUT_FAT_NOT_READY_FOR_SLEEP | int |  |
| OUT_FAT_EE_CHECKSUM_ERROR | int |  |
| OUT_FAT_DRIVE_ACK | int |  |
| OUT_FAT_POSITION | int |  |
| OUT_FAT_STROKELENGTH | unsigned int |  |
| OUT_FAT_OPENING_MM | unsigned int |  |
| OUT_DRIVE_COUNT_AFTER_INIT | unsigned int |  |
| OUT_FAT_STROKE_TIME | unsigned int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-var-iap-pwr-brose-control-bft"></a>
### _STATUS_VAR_IAP_PWR_BROSE_CONTROL_BFT

Auslesen der Stati von den Internen Variablen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2B Power Window EKS Brose $05 Control Variables BFT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IN_BFT_ENABLE_EKS | int |  |
| IN_BFT_DIRECTION | int |  |
| IN_BFT_DRIVE | int |  |
| IN_BFT_SHORT_LIFT | int |  |
| IN_BFT_DOORAJAR | int |  |
| IN_BFT_LOCKSTATE | int |  |
| IN_BFT_OTHER_WINDOW_STATE | int |  |
| IN_BFT_PANIC_ONE | int |  |
| IN_BFT_USASTANDART | int |  |
| IN_BFT_IGNITION_KEY | int | KL_15 |
| IN_BFT_KL_50 | int | KL_50 |
| IN_BFT_FH_MOTOR_P | int |  |
| IN_BFT_FH_MOTOR_M | int |  |
| IN_BFT_INITJOB | int |  |
| IN_BFT_ENABLE_TESTEKS | int |  |
| IN_PERFORMANCE_MEASUREMENT | int |  |
| IN_BFT_AUSENTEMP | int |  |
| IN_BFT_STANDZEIT | long |  |
| IN_BFT_SPEED | int |  |
| IN_BFT_TOPSTATUS | int |  |
| IN_BFT_VOLTAGE | int |  |
| IN_BFT_STOP_POSITION | unsigned int |  |
| IN_BFT_STROKELENGTH | unsigned int |  |
| IN_BFT_FETRAWE | int |  |
| LB_BFT_DENORMIEREN | int |  |
| LB_BFT_WAKEUPF | int |  |
| LB_BFT_POWER_ONF | int |  |
| BL_BFT_EE_WRITE_Z4 | int |  |
| BL_BFT_EE_WRITE_Z5 | int |  |
| BL_BFT_EE_WRITE_Z6 | int |  |
| BL_BFT_EE_WRITE_Z7 | int |  |
| BL_BFT_EE_WRITE_DLOG | int |  |
| BL_BFT_EE_WRITE_RLOG | int |  |
| OUT_BFT_CUTOUT | int |  |
| OUT_BFT_DRIVE | int |  |
| OUT_BFT_DIRECTION | int |  |
| OUT_BFT_AUTOMATIC | int |  |
| OUT_BFT_OVERHEAT90 | int |  |
| OUT_BFT_OVERHEAT100 | int |  |
| OUT_BFT_HALLDEFECT | int |  |
| OUT_BFT_HALL1DEFECT | int |  |
| OUT_BFT_HALL2DEFECT | int |  |
| OUT_BFT_RELAIS1DEFECT | int |  |
| OUT_BFT_RELAIS1VAL | int |  |
| OUT_BFT_RELAIS2DEFECT | int |  |
| OUT_BFT_RELAIS2VAL | int |  |
| OUT_BFT_NORMSTATE | int |  |
| OUT_BFT_DEBUGMODE | int |  |
| OUT_BFT_WINDOW_OPENED_COMPLETE | int |  |
| OUT_BFT_WINDOW_CLOSED_COMPLETE | int |  |
| OUT_BFT_NOT_READY_FOR_SLEEP | int |  |
| OUT_BFT_EE_CHECKSUM_ERROR | int |  |
| OUT_BFT_DRIVE_ACK | int |  |
| OUT_BFT_POSITION | int |  |
| OUT_BFT_STROKELENGTH | unsigned int |  |
| OUT_BFT_OPENING_MM | unsigned int |  |
| OUT_DRIVE_COUNT_AFTER_INIT | unsigned int |  |
| OUT_BFT_STROKE_TIME | unsigned int |  |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fh-adaptionsspeicher-loeschen"></a>
### STEUERN_FH_ADAPTIONSSPEICHER_LOESCHEN

Adaptionsdaten Fensterheber Loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $2C FH Adaptation Speicher loeschen $07 ShortTermAdjustment

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-marginal-read-flash"></a>
### _MARGINAL_READ_FLASH

Read out of marginal read compress value for flashROM KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $34 Marginal Read Flash

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BLOCK_A | int | Block if 128 Kb |
| CRC_LEVEL_A_0 | int | CRC Calculated with threshold in normal opperation |
| CRC_LEVEL_A_1 | int | CRC Calculated with threshold select value '01' |
| CRC_LEVEL_A_2 | int | CRC Calculated with threshold select value '10' |
| BLOCK_B | int | Block if 128 Kb |
| CRC_LEVEL_B_0 | int | CRC Calculated with threshold in normal opperation |
| CRC_LEVEL_B_1 | int | CRC Calculated with threshold select value '01' |
| CRC_LEVEL_B_2 | int | CRC Calculated with threshold select value '10' |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-diag-ringspeicher"></a>
### _READ_DIAG_RINGSPEICHER

KWP 2000: $21 ReadDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| POS_RINGSPEICHER | int | aktuelle POSITION im RINGSPEICHER |
| SCHALTER_LICHT_1 | int | Lichtschalterstellung 1 (Standlicht) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| SCHALTER_LICHT_2 | int | Lichtschalterstellung 2 (FLC) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| KL_15_HW | int | Klemme 15 HW-Eingang |
| KL_15_CAN | int | Klemme 15 ueber CAN |
| ANF_AL | int | Anforderung AL SW-seitig |
| AL_EINGANG_RED | int | redundanter Abblendlichteingang |
| RESET_COUNTER | int | RESET_COUNTER |
| BORDNETZ_SPG | real | BORDNETZ_SPG |
| GESCHWINDIGKEIT | int | GESCHWINDIGKEIT |
| KM_STAND | long | KM_STAND |
| TEL_STATUS_FAHRLICHT | long | TELEGRAMM STATUS_FAHRLICHT |
| ABS_TIMER | long | Absoluttimer im Steuergeraet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-diag-ringspeicher-lear"></a>
### _CLR_DIAG_RINGSPEICHER_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-diag-ringspeicher-reset"></a>
### _READ_DIAG_RINGSPEICHER_RESET

KWP 2000: $21 ReadDataByLocalIdentifier $0C DIAG_RESETSPEICHER Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| POS_RESETSPEICHER | int | aktuelle POSITION im RESETSPEICHER |
| SCHALTER_LICHT_1 | int | Lichtschalterstellung 1 (Standlicht) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| SCHALTER_LICHT_2 | int | Lichtschalterstellung 2 (FLC) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| KL_15_HW | int | Klemme 15 HW-Eingang |
| KL_15_CAN | int | Klemme 15 ueber CAN |
| ANF_AL | int | Anforderung AL SW-seitig |
| AL_EINGANG_RED | int | redundanter Abblendlichteingang |
| RESET_COUNTER | int | RESET_COUNTER |
| RESET_CAUSE | int | RESET_CAUSE |
| BORDNETZ_SPG | real | BORDNETZ_SPG |
| GESCHWINDIGKEIT | int | GESCHWINDIGKEIT |
| KM_STAND | long | KM_STAND |
| ABS_TIMER | long | Absoluttimer im Steuergeraet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-diag-resetpeicher-lear"></a>
### _CLR_DIAG_RESETPEICHER_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $0C DIAG_RESETSPEICHER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-output"></a>
### READ_ENERGY_OUTPUT

Read out the energy output data KWP 2000: $21 ReadDataByLocalIdentifier $0D ENERGY_OUTPUT Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KILOMETERSTAND | long | Milage |
| UBATT_START | real | Starting battery voltage |
| UBATT_ENDE | real | Ending battery voltage |
| TIMER | int | Time |
| TEMPERATUR | int | Temperatur |
| LICHT | int | Lights |
| SV_AUS | int | Power supply off |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-qualitaet-fensterheberlauf"></a>
### STATUS_QUALITAET_FENSTERHEBERLAUF

Qualitaetsbewertung Fensterheber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GRENZWERT_1 | int | Optional abweichender Grenzwert 1 |
| GRENZWERT_2 | int | Optional abweichender Grenzwert 2 |
| GRENZWERT_3 | int | Optional abweichender Grenzwert 3 |
| GRENZWERT_4 | int | Optional abweichender Grenzwert 4 |
| GRENZWERT_5 | int | Optional abweichender Grenzwert 5 |
| GRENZWERT_6 | int | Optional abweichender Grenzwert 6 |
| GRENZWERT_7 | int | Optional abweichender Grenzwert 7 |
| GRENZWERT_8 | int | Optional abweichender Grenzwert 8 |
| GRENZWERT_9 | int | Optional abweichender Grenzwert 9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| STAT_AUSWERTUNG_FAHRER | string | Interpretation Adaptionsdaten Fahrerseite Bei Kategorie 9, 8 und 7 wird die Oeffnungsweite des Fensters an der B-Saeule ausgegeben mit zugehoerigen Adaptionswert |
| STAT_KATEGORIE_FAHRER_WERT | int | Kategorie Fahrerseite als Integer |
| STAT_AUSWERTUNG_BEIFAHRER | string | Interpretation Adaptionsdaten Beifahrerseite Bei Kategorie 9, 8 und 7 wird die Oeffnungsweite des Fensters an der B-Saeule ausgegeben mit zugehoerigen Adaptionswert |
| STAT_KATEGORIE_BEIFAHRER_WERT | int | Kategorie Beifahrerseite als Integer |
| STAT_HUBZEIT_FAHRER | int | Hubzeit Fahrerseite in 10 ms |
| STAT_HUBZEIT_BEIFAHRER | int | Hubzeit Beifaherseite in 10 ms |
| STAT_AUSWERTUNG_HUBZEIT_FAHRER | string | Interpretation Hubzeit Fahrerseite |
| STAT_AUSWERTUNG_HUBZEIT_BEIFAHRER | string | Interpretation Hubzeit Beifahrerseite |
| STAT_ADAPTIONSDATEN_FAHRER | binary | ausgelesene Daten Fahrerseite |
| STAT_ADAPTIONSDATEN_BEIFAHRER | binary | ausgelesene Daten Beifahrerseite |
| STAT_INFO_GRENZWERTE | string | verwendete Grenzwerte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-adaptionsspeicher-lesen"></a>
### _STATUS_FH_ADAPTIONSSPEICHER_LESEN

Adaptionsdaten Fensterheber KWP2000: $30 InputOutputControlByLocalIdentifier $18 ECHTZEITDATEN_BROSE_LESEN $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ADAPTIONSDATEN_FAHRER | binary | ausgelesene Daten Fahrerseite |
| STAT_ADAPTIONSDATEN_BEIFAHRER | binary | ausgelesene Daten Beifahrerseite |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-reversierungs-logger-lesen-lear"></a>
### _STATUS_FH_REVERSIERUNGS_LOGGER_LESEN_LEAR

Fensterheber Reversierlogger auslesen KWP2000: $30 InputOutputControlByLocalIdentifier $2E _STATUS_FH_REVERSIERUNGS_LOGGER_LESEN $01 ReadCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REVERSIERUNGS_COUNTER | unsigned int | absolute Zahl der Reversierer, 0 - 65535 |
| STAT_DATENSATZ | string | Datensatz Nummer |
| STAT_FEHLERNUMMER | int | Fehlernummer des Reversierers |
| STAT_FEHLERNUMMER_TEXT | string | Fehlertext des Reversierers |
| STAT_POSITION_HZ | int | Scheibenposition in Hallsignale |
| STAT_VOLTAGE_WERT | real | Fensterheberspannung |
| STAT_AUSSENTEMP_WERT | real | Aussentemperatur in °C |
| STAT_SPEED_WERT | real | Fahrzeuggeschwindigkeit in km/h |
| _TEL_AUFTRAG | binary | Hex-Auftrag des Testers |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fh-reversierungs-logger-loeschen-lear"></a>
### _STEUERN_FH_REVERSIERUNGS_LOGGER_LOESCHEN_LEAR

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2E Reversierungslogger Status von FRMFA schreiben Loeschen von Reversierungslogger des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-digital"></a>
### STEUERN_LAMPEN_DIGITAL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von FRM II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Lampe aus Tabelle auswaehlen |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-pwm"></a>
### STEUERN_LAMPEN_PWM

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von FRM II schreiben Lampe mit Prozentwert ein- bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Lampe aus Tabelle auswaehlen |
| PWM_WERT | int | von 0 bis 100 in Prozent |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kindersicherung"></a>
### STEUERN_KINDERSICHERUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0D Kindersicherung Status von FRMFA schreiben Betaetigung des Kindersicherungstasters simulieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTER_KINDERSICHERUNG | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegelheizung-lear"></a>
### _STEUERN_SPIEGELHEIZUNG_LEAR

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0E Spiegelheizung Status von FRM-II schreiben Spiegelheizung mit speziellen Werten eischalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGELHEIZUNG_WERT | string | Wert fuer Spiegelheizung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegel-position"></a>
### STEUERN_SPIEGEL_POSITION

Ansteuerung Spiegel Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SPIEGEL | int | Auswahl des Spiegel 0: Fahrerspiegel 1: Beifahrerspiegel |
| RICHTUNG_SPIEGEL | int | Angabe Richtung 0x00: Vorgang abbrechen 0x01: Links 0x02: Oben 0x03: Rechts 0x04: Unten 0x05: Beiklappen |
| ANSTEUER_ZEIT_SPIEGEL | int | Ansteuerzeit in ms Nach 4 Sekunden wird die Ansteuerung automatisch beendet |

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

<a id="job-steuern-spiegel-abblenden"></a>
### STEUERN_SPIEGEL_ABBLENDEN

Ein bzw. Ausschalten der Spiegelheizung per Diagnose Max. Dauer 6 Sekunden mit ca. 60%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGEL_ABBLENDEN | int | 0: Abblenden ausschalten 1: Abblenden einschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-tuer"></a>
### STEUERN_DIGITAL_TUER

Ansteuerung der digitalen Eingaenge der Tuer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | string | Auswahl des Elements (ARGUMENT aus table STEUERN_DIGITAL_VERFAHREN) |
| AKTION | int | Aktion die durchgefuehrt werden soll Bei digitalen Ansteuerungen entweder 0 oder 1 Bei Ansteuerungen per Zeitangabe wird die Zeit in ms-Schritten angegeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber"></a>
### STEUERN_FENSTERHEBER

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0A Ansteuern FH Status von FRMFA schreiben Verfahren der Fensterheber, Fahrer, Beifahrer, beide

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG_FH_FAT | string | table FH_Richtung NAME TEXT Auswahl der Richtung, in der das Fahrertuerfenster verfahren soll |
| ANSTEUER_ZEIT_FAT | int | Zeit in 100ms, die der FH angesteuert werden soll, d.h. 1 = 100ms |
| RICHTUNG_FH_BFT | string | table FH_Richtung NAME TEXT Auswahl der Richtung, in der das Beiahrertuerfenster verfahren soll |
| ANSTEUER_ZEIT_BFT | int | Zeit in 100ms, die der FH angesteuert werden soll, d.h. 1 = 100ms |
| IM_PANIK_MODUS | int | Ansteuern der FH im Panikmodus Stufe 1 0 = Normalmodus, 1 = Panikmodus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-einlernen-ohne-eks"></a>
### STEUERN_FENSTERHEBER_EINLERNEN_OHNE_EKS

Einlernen der Fensterheber Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER  ARGUMENT BESCHREIBUNG) 0x00: Vorgang abbrechen 0x11: Fahrerseite 0x12: Beifahrerseite 0x21: Fahrerseite und Beifahrerseite 0x40: Alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_VORGANG_GESTARTET_EIN | int | 0: Einlernvorgang konnte nicht gestartet werden 1: Einlernvorgang gestartet |
| STATUS_VORGANG_GESTARTET_DEZIMAL | int | Zuordnung siehe CODE aus table FH_EINLERNEN  CODE BESCHREIBUNG siehe STATUS_VORGANG_GESTARTET_TEXT |
| STATUS_VORGANG_GESTARTET_TEXT | string | Zuordnung siehe BESCHREIBUNG aus table FH_EINLERNEN  CODE BESCHREIBUNG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-einlernen"></a>
### STEUERN_FENSTERHEBER_EINLERNEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $19 Ansteuern FH Status von FRM II schreiben Dauer max. 7sec Einlernen der Fensterheber mit EKS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER  ARGUMENT BESCHREIBUNG) 0x00: Vorgang abbrechen 0x11: Fahrerseite 0x12: Beifahrerseite 0x21: Fahrerseite und Beifahrerseite 0x40: Alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_VORGANG_GESTARTET_EIN | int | 0: Einlernvorgang konnte nicht gestartet werden 1: Einlernvorgang gestartet |
| STATUS_VORGANG_GESTARTET_DEZIMAL | int | Zuordnung siehe CODE aus table FH_EINLERNEN  CODE BESCHREIBUNG siehe STATUS_VORGANG_GESTARTET_TEXT |
| STATUS_VORGANG_GESTARTET_TEXT | string | Zuordnung siehe BESCHREIBUNG aus table FH_EINLERNEN  CODE BESCHREIBUNG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-denormieren"></a>
### STEUERN_FENSTERHEBER_DENORMIEREN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $19 Ansteuern FH Status von FRM II schreiben Dauer max. 7sec Einlernen der Fensterheber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER  ARGUMENT BESCHREIBUNG) 0x00: Vorgang abbrechen 0x11: Fahrerseite 0x12: Beifahrerseite 0x21: Fahrerseite und Beifahrerseite 0x40: Alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-al-einschalten"></a>
### STEUERN_AL_EINSCHALTEN

Abblendlicht ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0F Abblendlicht ein- bzw. ausschalten Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AL_EIN_AUS | string | Werte: ein, aus table DigitalArgument TEXT |
| AL_ZEIT | int | Werte: 0 bis 254 Einheit: secons Optional argument, by default is 15 sec. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-funktionen-einschalten"></a>
### STEUERN_LAMPEN_FUNKTIONEN_EINSCHALTEN

Lampenfunktionen ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $29 Lampenfunktionen ein- bzw. ausschalten Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_LAMPEN_FUNKTION | string | Lampen group table LampFunkTexte NAME |
| LAMPEN_EIN_AUS | string | Werte: ein, aus table DigitalArgument TEXT |
| EINSCHALT_ZEIT | int | Werte: 0 bis 254 Einheit: secons Optional argument, by default is 15 sec. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-direkt-spiegel"></a>
### STEUERN_POSITION_DIREKT_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $12 Position Spiegel fuer FRMFA Status von FRM-II schreiben ausgewaehlten Spiegel in angegebene Position fahren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SPIEGEL | string | table Auswahl_Spiegel NAME TEXT Spiegel auswaehlen |
| RICHTUNG_SPIEGEL_HORIZONTAL | int |  |
| RICHTUNG_SPIEGEL_VERTIKAL | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegel-abblenden-lear"></a>
### _STEUERN_SPIEGEL_ABBLENDEN_LEAR

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $11 SPIEGEL_ABBLENDEN Status von FRM-II schreiben Abblenden der Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGEL_ABBLENDEN_WERT | int | Wert wie Aussenspiegel abgeblendet werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-memory-position-spiegel"></a>
### STEUERN_MEMORY_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0C Position Spiegel fuer FRMFA Status von PL4-FRM II schreiben Schreiben der MemoryPosition der beiden Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY | int | 0 bis 3 und 255 welcher Schluessel |
| MEM_POS_SLOT | int | 0 bis 3 welche Memoryposition |
| MEM_POS_SPIEGEL_FAHRER_HOR_WERT | int | Position Fahrerspiegel horizontal |
| MEM_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Position Beifahrerspiegel horizontal |
| MEM_POS_SPIEGEL_FAHRER_VER_WERT | int | Position Fahrerspiegel vertikal |
| MEM_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Position Beifahrerspiegel vertikal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-innenbeleuchtung-daueraus"></a>
### STEUERN_INNENBELEUCHTUNG_DAUERAUS

KWP2000: $30 InputOutputControlByLocalIdentifier $08 LongTermAdjustment $26 Innenbeleuchtung Dauerausschalten Innenbeleuchtung Dauerausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INNENBELEUCHTUNG_DAUERAUS_EIN | string | Werte: ein, aus table DigitalArgument TEXT Innenbeleuchtung Dauerausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-messdaten-aktivieren"></a>
### STEUERN_FENSTERHEBER_MESSDATEN_AKTIVIEREN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1E Ansteuern FH Messdatenausgabe fuer FH starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FENSTER | int | Auswahl des Fensterhebers (ARGUMENT aus table AUSWAHL_FENSTER  ARGUMENT BESCHREIBUNG) 0x00: Vorgang abbrechen 0x11: Fahrerseite 0x12: Beifahrerseite 0x13: Fahrerseite hinten 0x14: Beifahrerseite hinten 0x21: Fahrerseite und Beifahrerseite 0x22: Fahrerseite und Beifahrerseite hinten 0x40: Alle Nicht zutreffendes entfernen!!!!! Auch aus der Tabelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bfd-stufe"></a>
### STEUERN_BFD_STUFE

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $24 BFD-Stufe ein-/ausschalten Status von FRM II schreiben Ausgewaehlte BFD-Stufe ein bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table BFDStufeTexte NAME TEXT BFD-Stufe aus Tabelle auswaehlen |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-lwr"></a>
### STEUERN_POSITION_LWR

bestimmte Position der LWR anfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $09 Position der LWR anfahren Status von FRM II schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POS_LWR | long | Winkel fuer LWR Einstellung in 1/100 Grad max. bzw. min. kann mit STATUS_LWR_LESEN ausgelesen werden |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kurzhub-deaktivieren"></a>
### STEUERN_KURZHUB_DEAKTIVIEREN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2D Kurzhub Deaktivieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTIV | int | EIN: Kurzhub deaktiviren AUS: Kurzhub reaktiviren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-innenbeleuchtung"></a>
### STEUERN_INNENBELEUCHTUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2F Innenbeleuchtung Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VORFELDBELEUCHTUNG | string | Werte: ein, aus table DigitalArgument TEXT |
| INNENBELEUCHTUNG | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-lampen-pre-drive-check"></a>
### START_LAMPEN_PRE_DRIVE_CHECK

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $31 Start des Pre-Drive-Checks der Lampen Status von FRMFA schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-led-digital"></a>
### STEUERN_LED_DIGITAL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $35 Dimmwert an LED Status von FRM II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LEDNrTexte NAME TEXT Lampe aus Tabelle auswaehlen |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-led-pwm"></a>
### STEUERN_LED_PWM

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $35 Dimmwert an PWM-Port Status von FRM II schreiben Lampe mit Prozentwert ein- bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LEDNrTexte NAME TEXT Lampe aus Tabelle auswaehlen |
| PWM_WERT | int | von 0 bis 100 in Prozent |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bixenon-klappe-digital"></a>
### STEUERN_BIXENON_KLAPPE_DIGITAL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $36 Dimmwert an LED Status von FRM II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-smc-bestromen"></a>
### STEUERN_SMC_BESTROMEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1A SMC bestromen Status von FRM-II schreiben Bestromung der SMCs einschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BESTROMEN_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-referenzlauf-alc-system"></a>
### STEUERN_REFERENZLAUF_ALC_SYSTEM

Referenzlauf der SMCs starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REFERENZLAUF | string | Referenzlauf fuer Kurvenlicht auswaehlen falls keiner ausgewaehlt dann wird mit Sensor ausgewaehlt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-referenzlauf-alc-system"></a>
### STATUS_REFERENZLAUF_ALC_SYSTEM

Pruefung, ob ALC-System referenziert ist KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ALC_SYSTEM_REFERENZIERT_EIN | int | gibt an ob ALC-System fertig referenziert hat |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-block-schreiben-lear"></a>
### _CODIERDATEN_SMC_BLOCK_SCHREIBEN_LEAR

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
### _CODIERDATEN_SMC_SCHREIBEN_LEAR

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
### _CODIERDATEN_SMC_BLOCK_LESEN_LEAR

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
### _CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR

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
### _CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR

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

Schreiben der VIN in die linke SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die linke SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VINDATEN | string | 7stellige Fahrgestellnummern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vin-smc-rechts-schreiben-lear"></a>
### VIN_SMC_RECHTS_SCHREIBEN_LEAR

Schreiben der VIN in die rechte SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die rechte SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VINDATEN | string | 7stellige Fahrgestellnummern |

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

ID-SMC lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-SMC Modus  : Default Auslesen der Identdaten der SMCs

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
| STAT_POS_KURVENLICHT | long | Winkel fuer Kurvenlicht je nach Scheinwerfer max. von -170 bis 170 entspricht -17Grad bis 17Grad |
| STAT_POS_LWR | long | Winkel fuer LWR je nach Scheinwerfer max. von 0 bis 1000 entspricht 0Grad bis 10Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-smc"></a>
### STEUERN_POSITION_SMC

bestimmte Position der SMC anfahren KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht starten $41 Pos LWR starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| POS_KURVENLICHT | long | Winkel fuer Kurvenlicht je nach Scheinwerfer max. von -170 bis 170 entspricht -17Grad bis 17Grad |
| GESCHW_KURVENLICHT | unsigned char | Geschwindigkeit fuer Kurvenlicht je nach Scheinwerfer max. von 0 bis 31 |
| POS_LWR | long | Winkel fuer LWR je nach Scheinwerfer max. von 0 bis 1000 entspricht 0Grad bis 10Grad |
| GESCHW_LWR | unsigned char | Geschwindigkeit fuer LWR je nach Scheinwerfer max. von 0 bis 7 |

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
### _HERSTELLERDATEN_SMC_LEAR_SCHREIBEN

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
### _HERSTELLERDATEN_SMC_LEAR_LESEN

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

Infospeicher von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

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

Infospeicher von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

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

Infospeicher Details von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt Es darf dann nicht argument F_POS angegeben werden |
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

Infospeicher Details von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt Es darf dann nicht argument F_POS angegeben werden |
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

Infospeicher der SMC links loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen-smc-r-lear"></a>
### IS_LOESCHEN_SMC_R_LEAR

Infospeicher der SMC rechts loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-smc"></a>
### STATUS_BETR_H_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $51 Betriebsstunden Betriebsstunden von ausgewaehlter SMC lesen

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $51 Betriebsstunden alle Betriebszeiten der ausgewaehlten SMC loeschen

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $50 Verteilung der Winkelansteuerung Verteilung der Winkelansteuerung von ausgewaehlter SMC lesen

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $50 Verteilung der Winkelansteuerung Loeschen der Verteilung der Winkelansteuerung der ausgewaehlten SMC

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $52 Temperaturverteilung Temperaturverteilung von der ausgewaehlten SMC lesen

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $52 Temperaturverteilung Loeschen der Temperaturverteilung der ausgewaehlten SMC

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $53 Schrittverluste Schrittverluste von der ausgewaehlten SMC lesen

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $53 Schrittverluste Loeschen der Schrittverluste der ausgewaehlten SMC

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

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $54 HW_Eingaenge HW_Eingaenge von der ausgewaehlten SMC lesen

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
### _HERSTELLERTEST_SMC_LEAR

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

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
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
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (88 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (86 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (11 × 9)
- [HORTTEXTE](#table-horttexte) (81 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (80 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (12 × 9)
- [IORTTEXTE](#table-iorttexte) (38 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [LAMPNRTEXTE](#table-lampnrtexte) (33 × 3)
- [ACTIVETAB](#table-activetab) (3 × 2)
- [SPIEGEL_HEIZUNG](#table-spiegel-heizung) (9 × 3)
- [SPIEGELHEIZUNGSTAT](#table-spiegelheizungstat) (9 × 2)
- [FH_RICHTUNG](#table-fh-richtung) (4 × 3)
- [AUSWAHL_FENSTER](#table-auswahl-fenster) (5 × 2)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [AUSWAHL_SPIEGEL](#table-auswahl-spiegel) (3 × 3)
- [RICHTUNG_SPIEGEL](#table-richtung-spiegel) (7 × 3)
- [STEUERN_DIGITAL_VERFAHREN](#table-steuern-digital-verfahren) (16 × 3)
- [TIEFENTL](#table-tiefentl) (1 × 8)
- [SMCS](#table-smcs) (3 × 3)
- [REF_SMCS](#table-ref-smcs) (4 × 3)
- [NOTL](#table-notl) (1 × 7)
- [FH_DENORM_FEHLERTEXTE](#table-fh-denorm-fehlertexte) (26 × 2)
- [BFDSTUFETEXTE](#table-bfdstufetexte) (9 × 3)
- [FH_EINLERNEN](#table-fh-einlernen) (7 × 2)
- [STAT_LENKSTOCK_BLINKER](#table-stat-lenkstock-blinker) (13 × 3)
- [STAT_LAMPEN_DEFEKTE](#table-stat-lampen-defekte) (4 × 3)
- [LAMPFUNKTEXTE](#table-lampfunktexte) (10 × 3)
- [FH_REVERSIER_FEHLERTEXTE](#table-fh-reversier-fehlertexte) (8 × 2)
- [EKS_HERSTELLER](#table-eks-hersteller) (4 × 2)
- [KUESTER_EE_DENORM_LOG](#table-kuester-ee-denorm-log) (36 × 2)
- [LEDNRTEXTE](#table-lednrtexte) (4 × 3)

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

Dimensions: 88 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9CA8 | interner Fehler |
| 0x9CA9 | Klemme 30A Anschluss fehlerhaft |
| 0x9CAA | Klemme 30B Anschluss fehlerhaft |
| 0x9CAB | eine Klemme 15 fehlt |
| 0x9CAC | Bremslichtschalter defekt |
| 0x9CAD | Energiesparmode aktiv |
| 0x9CAE | Colourswitch fehlerhaft |
| 0x9CAF | Lichtschalterstellung 1 defekt |
| 0x9CB0 | Lichtschalterstellung 2 defekt |
| 0x9CB1 | Dimmer-Poti defekt |
| 0x9CB2 | LWR-Poti defekt |
| 0x9CB3 | Sensor Hoehenstand vorne defekt |
| 0x9CB4 | Sensor Hoehenstand hinten defekt |
| 0x9CB5 | Batterie tiefentladen |
| 0x9CB6 | LWR-Spulenabriss |
| 0x9CB7 | LWR-Treiberfehler |
| 0x9CB8 | Tiefentladungsschutz der Batterie: Abschaltung Standlicht |
| 0x9CB9 | Tiefentladungsschutz der Batterie: Abschaltung Parklicht |
| 0x9CBA | Kommunikation mit LIN-Bedienteil gestoert |
| 0x9CBB | Kurzschlussfehler |
| 0x9CBC | Kurschluss Tuerkontakte vorne |
| 0x9CBD | Kurschluss Tuerkontakte hinten |
| 0x9CBE | Bedienteilfehler |
| 0x9CBF | Kommunikation mit StepperMoterBox links gestoert |
| 0x9CC0 | Kommunikation mit StepperMoterBox rechts gestoert |
| 0x9CC1 | Achtung: Elektronik am linken Scheinwerfer (SMC) meldet Fehler |
| 0x9CC2 | Achtung: Elektronik am rechten Scheinwerfer (SMC) meldet Fehler |
| 0x9CC3 | Kommunikation mit Spiegel Fahrerseite gestoert |
| 0x9CC4 | Kommunikation mit Spiegel Beifahrerseite gestoert |
| 0x9CC5 | Spiegelheizung Fahrerseite defekt |
| 0x9CC6 | Spiegelheizung Beifahrerseite defekt |
| 0x9CC7 | Hallsensor FH-Fahrertuer defekt |
| 0x9CC8 | Hallsensor FH-Beifahrertuer defekt |
| 0x9CC9 | Zeitfenster FH-Fahrertuer gestoert |
| 0x9CCA | Zeitfenster FH-Beifahrertuer gestoert |
| 0x9CCB | Relais FH-Fahrertuer defekt |
| 0x9CCC | Relais FH-Beifahrertuer defekt |
| 0x9CCD | Antrieb Spiegel Fahrerseite defekt |
| 0x9CCE | Antrieb Spiegel Beifahrerseite defekt |
| 0x9CCF | Antrieb Beiklappen Spiegel Fahrerseite defekt |
| 0x9CD0 | Antrieb Beiklappen Spiegel Beifahrerseite defekt |
| 0x9CD1 | Vergleich Fahrgestellnummer ALC mit SMC links unterschiedlich |
| 0x9CD2 | Vergleich Fahrgestellnummer ALC mit SMC rechts unterschiedlich |
| 0x9CD3 | Unkonsistenz: Softwareversion und Codierindex |
| 0xA8A8 | Fernlicht links defekt |
| 0xA8A9 | Fernlicht rechts defekt |
| 0xA8AA | Abblendlicht links defekt |
| 0xA8AB | Abblendlicht rechts defekt |
| 0xA8AC | Begrenzungslicht links defekt |
| 0xA8AD | Begrenzungslicht rechts defekt |
| 0xA8AE | Nebelscheinwerfer links defekt |
| 0xA8AF | Nebelscheinwerfer rechts defekt |
| 0xA8B0 | Fahrtrichtungsanzeiger links vorne defekt |
| 0xA8B1 | Fahrtrichtungsanzeiger rechts vorne defekt |
| 0xA8B2 | Fahrtrichtungsanzeiger links hinten defekt |
| 0xA8B3 | Fahrtrichtungsanzeiger rechts hinten defekt |
| 0xA8B4 | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange defekt |
| 0xA8B5 | E70: Seitenmarkierungsleuchte rechts vorne, R56: Colour-Switch Blau defekt |
| 0xA8B6 | Bremslicht links defekt |
| 0xA8B7 | Bremslicht rechts defekt |
| 0xA8B8 | Bremslicht mitte defekt |
| 0xA8B9 | Schlusslicht links 1 defekt |
| 0xA8BA | Schlusslicht rechts 1 defekt |
| 0xA8BB | E70: Schlusslicht links 2, R56: Seitenmarkierungsleuchte links vorne, rechts hinten defekt |
| 0xA8BC | E70: Schlusslicht rechts 2, R56: Seitenmarkierungsleuchte rechts vorne, links hinten defekt |
| 0xA8BD | Kennzeichenlicht defekt |
| 0xA8BE | Innenbeleuchtung defekt |
| 0xA8BF | Nebelschlusslicht links defekt |
| 0xA8C0 | Nebelschlusslicht rechts |
| 0xA8C1 | Rueckfahrlicht links defekt |
| 0xA8C2 | Rueckfahrlicht rechts defekt |
| 0xA8C3 | Break-Force-Display links defekt |
| 0xA8C4 | Break-Force-Display rechts defekt |
| 0xA8C5 | Tagfahrlicht links defekt |
| 0xA8C6 | Tagfahrlicht rechts defekt |
| 0xA8C7 | Klemme 58g defekt |
| 0xE584 | Bus Leitungsfehler K-CAN |
| 0xE587 | Bus Kommunikationsfehler K-CAN |
| 0xE594 | Telegramm Lenkwinkel Timeout |
| 0xE595 | Telegramm Status-AHM Timeout |
| 0xE596 | Telegramm Fernlichtassistent Timeout |
| 0xE597 | Telegramm Status DSC Timeout |
| 0xE598 | Telegramm Status Fahrlicht Timeout |
| 0xE599 | Telegramm Geschwindigkeit Timeout |
| 0xE59A | Telegramm Gierrate Timeout |
| 0xE59B | Telegramm Klemmenstatus Timeout |
| 0xE59C | Telegramm PT-CAN Lenkwinkel Timeout |
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

Dimensions: 86 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9CA8 | 0x01 | 0x02 | - | - |
| 0x9CA9 | 0x01 | 0x02 | - | - |
| 0x9CAA | 0x01 | 0x02 | - | - |
| 0x9CAB | 0x01 | 0x02 | - | - |
| 0x9CAC | 0x01 | 0x02 | - | - |
| 0x9CAD | 0x01 | 0x02 | - | - |
| 0x9CAE | 0x01 | 0x02 | - | - |
| 0x9CAF | 0x01 | 0x02 | - | - |
| 0x9CB0 | 0x01 | 0x02 | - | - |
| 0x9CB1 | 0x01 | 0x02 | - | - |
| 0x9CB2 | 0x01 | 0x02 | - | - |
| 0x9CB3 | 0x01 | 0x02 | - | - |
| 0x9CB4 | 0x01 | 0x02 | - | - |
| 0x9CB5 | 0x01 | TIEFENTL | - | - |
| 0x9CB6 | 0x01 | 0x02 | - | - |
| 0x9CB7 | 0x01 | 0x02 | - | - |
| 0x9CB8 | 0x01 | 0x02 | - | - |
| 0x9CB9 | 0x01 | 0x02 | - | - |
| 0x9CBA | 0x01 | 0x02 | - | - |
| 0x9CBB | 0x01 | 0x02 | - | - |
| 0x9CBC | 0x01 | 0x02 | - | - |
| 0x9CBD | 0x01 | 0x02 | - | - |
| 0x9CBE | 0x01 | 0x02 | - | - |
| 0x9CBF | 0x01 | 0x02 | - | - |
| 0x9CC0 | 0x01 | 0x02 | - | - |
| 0x9CC1 | 0x01 | 0x02 | - | - |
| 0x9CC2 | 0x01 | 0x02 | - | - |
| 0x9CC3 | 0x01 | 0x02 | - | - |
| 0x9CC4 | 0x01 | 0x02 | - | - |
| 0x9CC5 | 0x01 | 0x02 | - | - |
| 0x9CC6 | 0x01 | 0x02 | - | - |
| 0x9CC7 | 0x01 | 0x02 | - | - |
| 0x9CC8 | 0x01 | 0x02 | - | - |
| 0x9CC9 | 0x01 | 0x02 | - | - |
| 0x9CCA | 0x01 | 0x02 | - | - |
| 0x9CCB | 0x01 | 0x02 | - | - |
| 0x9CCC | 0x01 | 0x02 | - | - |
| 0x9CCD | 0x01 | 0x02 | - | - |
| 0x9CCE | 0x01 | 0x02 | - | - |
| 0x9CCF | 0x01 | 0x02 | - | - |
| 0x9CD0 | 0x01 | 0x02 | - | - |
| 0x9CD1 | 0x01 | 0x02 | - | - |
| 0x9CD2 | 0x01 | 0x02 | - | - |
| 0xA8A8 | 0x01 | 0x03 | - | - |
| 0xA8A9 | 0x01 | 0x03 | - | - |
| 0xA8AA | 0x01 | 0x03 | - | - |
| 0xA8AB | 0x01 | 0x03 | - | - |
| 0xA8AC | 0x01 | 0x03 | - | - |
| 0xA8AD | 0x01 | 0x03 | - | - |
| 0xA8AE | 0x01 | 0x03 | - | - |
| 0xA8AF | 0x01 | 0x03 | - | - |
| 0xA8B0 | 0x01 | 0x03 | - | - |
| 0xA8B1 | 0x01 | 0x03 | - | - |
| 0xA8B2 | 0x01 | 0x03 | - | - |
| 0xA8B3 | 0x01 | 0x03 | - | - |
| 0xA8B4 | 0x01 | 0x03 | - | - |
| 0xA8B5 | 0x01 | 0x03 | - | - |
| 0xA8B6 | 0x01 | 0x03 | - | - |
| 0xA8B7 | 0x01 | 0x03 | - | - |
| 0xA8B8 | 0x01 | 0x03 | - | - |
| 0xA8B9 | 0x01 | 0x03 | - | - |
| 0xA8BA | 0x01 | 0x03 | - | - |
| 0xA8BB | 0x01 | 0x03 | - | - |
| 0xA8BC | 0x01 | 0x03 | - | - |
| 0xA8BD | 0x01 | 0x03 | - | - |
| 0xA8BE | 0x01 | 0x03 | - | - |
| 0xA8BF | 0x01 | 0x03 | - | - |
| 0xA8C0 | 0x01 | 0x03 | - | - |
| 0xA8C1 | 0x01 | 0x03 | - | - |
| 0xA8C2 | 0x01 | 0x03 | - | - |
| 0xA8C3 | 0x01 | 0x03 | - | - |
| 0xA8C4 | 0x01 | 0x03 | - | - |
| 0xA8C5 | 0x01 | 0x03 | - | - |
| 0xA8C6 | 0x01 | 0x03 | - | - |
| 0xA8C7 | 0x01 | 0x03 | - | - |
| 0xE584 | 0x01 | 0x02 | - | - |
| 0xE587 | 0x01 | 0x02 | - | - |
| 0xE594 | 0x01 | 0x02 | - | - |
| 0xE595 | 0x01 | 0x02 | - | - |
| 0xE596 | 0x01 | 0x02 | - | - |
| 0xE597 | 0x01 | 0x02 | - | - |
| 0xE598 | 0x01 | 0x02 | - | - |
| 0xE599 | 0x01 | 0x02 | - | - |
| 0xE59A | 0x01 | 0x02 | - | - |
| 0xE59B | 0x01 | 0x02 | - | - |
| 0xE59C | 0x01 | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 11 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x02 | Sensorspannung | Volt | - | unsigned char | - | 5 | 255 | 0 |
| 0x03 | Betriebsstunden | h | - | unsigned char | - | 2 | 1 | 0 |
| 0x10 | Klemme 15 | 0/1 | high | 0x80 | - | 1 | 1 | 0 |
| 0x11 | Klemme R | 0/1 | high | 0x40 | - | 1 | 1 | 0 |
| 0x12 | Standlicht | 0/1 | high | 0x20 | - | 1 | 1 | 0 |
| 0x13 | Parklicht links | 0/1 | high | 0x10 | - | 1 | 1 | 0 |
| 0x14 | Parklicht rechts | 0/1 | high | 0x08 | - | 1 | 1 | 0 |
| 0x15 | Warnblinklicht | 0/1 | high | 0x04 | - | 1 | 1 | 0 |
| 0x16 | Follow me home | 0/1 | high | 0x02 | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 81 rows × 2 columns

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
| 0x9400 | EEPROM SMC links defekt |
| 0x9401 | Motor Kurvenlicht SMC links defekt |
| 0x9402 | Motor LWR SMC links defekt |
| 0x9403 | Treiber Kurvenlicht SMC links defekt |
| 0x9404 | Spannungsversorgung Sensor SMC links defekt |
| 0x9405 | Signal Sensor SMC links defekt |
| 0x9406 | Flanke Sensor SMC links defekt |
| 0x9407 | LIN SMC links defekt |
| 0x9408 | Schrittverlust Grenze 1 SMC links |
| 0x9409 | Schrittverlust Grenze 2 SMC links |
| 0x940A | Schrittverlust Grenze 3 SMC links |
| 0x940B | Schrittverlust Grenze 4 SMC links |
| 0x940C | Schrittverlust Grenze 5 SMC links |
| 0x940D | Schrittverlust Grenze 6 SMC links |
| 0x940E | Spike auf Sensor SMS links |
| 0x940F | Notlauf aktiv SMC links |
| 0x9410 | unbekannter Fehler 2 SMC links |
| 0x9411 | unbekannter Fehler 3 SMC links |
| 0x9412 | unbekannter Fehler 4 SMC links |
| 0x9413 | unbekannter Fehler 5 SMC links |
| 0x9420 | EEPROM SMC rechts defekt |
| 0x9421 | Motor Kurvenlicht SMC rechts defekt |
| 0x9422 | Motor LWR SMC rechts defekt |
| 0x9423 | Treiber Kurvenlicht SMC rechts defekt |
| 0x9424 | Spannungsversorgung Sensor SMC rechts defekt |
| 0x9425 | Signal Sensor SMC rechts defekt |
| 0x9426 | Flanke Sensor SMC rechts defekt |
| 0x9427 | LIN SMC rechts defekt |
| 0x9428 | Schrittverlust Grenze 1 SMC rechts |
| 0x9429 | Schrittverlust Grenze 2 SMC rechts |
| 0x942A | Schrittverlust Grenze 3 SMC rechts |
| 0x942B | Schrittverlust Grenze 4 SMC rechts |
| 0x942C | Schrittverlust Grenze 5 SMC rechts |
| 0x942D | Schrittverlust Grenze 6 SMC rechts |
| 0x942E | Spike auf Sensor SMS rechts |
| 0x942F | Notlauf aktiv SMC rechts |
| 0x9430 | unbekannter Fehler 2 SMC rechts |
| 0x9431 | unbekannter Fehler 3 SMC rechts |
| 0x9432 | unbekannter Fehler 4 SMC rechts |
| 0x9433 | unbekannter Fehler 5 SMC rechts |
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
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 80 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9308 | 0x04 | -- | -- | -- |
| 0x9309 | 0x01 | -- | -- | -- |
| 0x930A | 0x01 | -- | -- | -- |
| 0x930B | 0x01 | -- | -- | -- |
| 0x930C | 0x03 | -- | -- | -- |
| 0x930D | 0x01 | -- | -- | -- |
| 0x930E | 0x01 | -- | -- | -- |
| 0x930F | 0x01 | -- | -- | -- |
| 0x9310 | 0x01 | -- | -- | -- |
| 0x9311 | 0x01 | -- | -- | -- |
| 0x9312 | 0x01 | -- | -- | -- |
| 0x9313 | 0x01 | -- | -- | -- |
| 0x9314 | 0x01 | -- | -- | -- |
| 0x9315 | 0x01 | -- | -- | -- |
| 0x9316 | 0x03 | -- | -- | -- |
| 0x9317 | NOTL | -- | -- | -- |
| 0x9318 | -- | -- | -- | -- |
| 0x9319 | -- | -- | -- | -- |
| 0x931A | -- | -- | -- | -- |
| 0x931B | -- | -- | -- | -- |
| 0x931C | 0x04 | -- | -- | -- |
| 0x931D | 0x01 | -- | -- | -- |
| 0x931E | 0x01 | -- | -- | -- |
| 0x931F | 0x01 | -- | -- | -- |
| 0x9320 | 0x03 | -- | -- | -- |
| 0x9321 | 0x01 | -- | -- | -- |
| 0x9322 | 0x01 | -- | -- | -- |
| 0x9323 | 0x01 | -- | -- | -- |
| 0x9324 | 0x01 | -- | -- | -- |
| 0x9325 | 0x01 | -- | -- | -- |
| 0x9326 | 0x01 | -- | -- | -- |
| 0x9327 | 0x01 | -- | -- | -- |
| 0x9328 | 0x01 | -- | -- | -- |
| 0x9329 | 0x01 | -- | -- | -- |
| 0x932A | 0x03 | -- | -- | -- |
| 0x932B | NOTL | -- | -- | -- |
| 0x932C | -- | -- | -- | -- |
| 0x932D | -- | -- | -- | -- |
| 0x932E | -- | -- | -- | -- |
| 0x932F | -- | -- | -- | -- |
| 0x9400 | 0x04 | -- | -- | -- |
| 0x9401 | 0x01 | -- | -- | -- |
| 0x9402 | 0x01 | -- | -- | -- |
| 0x9403 | 0x01 | -- | -- | -- |
| 0x9404 | 0x03 | -- | -- | -- |
| 0x9405 | 0x01 | -- | -- | -- |
| 0x9406 | 0x01 | -- | -- | -- |
| 0x9407 | 0x01 | -- | -- | -- |
| 0x9408 | 0x01 | -- | -- | -- |
| 0x9409 | 0x01 | -- | -- | -- |
| 0x940A | 0x01 | -- | -- | -- |
| 0x940B | 0x01 | -- | -- | -- |
| 0x940C | 0x01 | -- | -- | -- |
| 0x940D | 0x01 | -- | -- | -- |
| 0x940E | 0x03 | -- | -- | -- |
| 0x940F | NOTL | -- | -- | -- |
| 0x9410 | -- | -- | -- | -- |
| 0x9411 | -- | -- | -- | -- |
| 0x9412 | -- | -- | -- | -- |
| 0x9413 | -- | -- | -- | -- |
| 0x9420 | 0x04 | -- | -- | -- |
| 0x9421 | 0x01 | -- | -- | -- |
| 0x9422 | 0x01 | -- | -- | -- |
| 0x9423 | 0x01 | -- | -- | -- |
| 0x9424 | 0x03 | -- | -- | -- |
| 0x9425 | 0x01 | -- | -- | -- |
| 0x9426 | 0x01 | -- | -- | -- |
| 0x9427 | 0x01 | -- | -- | -- |
| 0x9428 | 0x01 | -- | -- | -- |
| 0x9429 | 0x01 | -- | -- | -- |
| 0x942A | 0x01 | -- | -- | -- |
| 0x942B | 0x01 | -- | -- | -- |
| 0x942C | 0x01 | -- | -- | -- |
| 0x942D | 0x01 | -- | -- | -- |
| 0x942E | 0x03 | -- | -- | -- |
| 0x942F | NOTL | -- | -- | -- |
| 0x9430 | -- | -- | -- | -- |
| 0x9431 | -- | -- | -- | -- |
| 0x9432 | -- | -- | -- | -- |
| 0x9433 | -- | -- | -- | -- |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x02 | Betriebsstunden | min | - | unsigned int | - | 3 | 1 | 0 |
| 0x03 | Sensorspannung | Volt | - | unsigned char | - | 5 | 255 | 0 |
| 0x04 | Motortemperatur | °C | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Bordnetzspannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x10 | NOT_SENS_DEFEKT | 0/1 | high | 0x01 | - | 1 | 1 | 0 |
| 0x11 | NOT_SENS_NOK | 0/1 | high | 0x02 | - | 1 | 1 | 0 |
| 0x12 | NOT_SCHR_VER_NOK | 0/1 | high | 0x04 | - | 1 | 1 | 0 |
| 0x13 | NOT_USENS_NOK | 0/1 | high | 0x08 | - | 1 | 1 | 0 |
| 0x14 | NOT_MOTOR_DEF | 0/1 | high | 0x10 | - | 1 | 1 | 0 |
| 0x15 | NOT_MOTOR_LWR_DEF | 0/1 | high | 0x20 | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 38 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | LoadDump aktiviert |
| 0x9309 | Kommunikation mit Co-Micro gestoert |
| 0x930A | Sleepmode Co-Micro gestoert |
| 0x930B | Lesen der Ports Co-Micro gestoert |
| 0x930C | Wakeup-Reason Co-Micro gestoert |
| 0x930D | Lesen des Interface Co-Micro gestoert |
| 0x930E | Schreiben des Interface Co-Micro gestoert |
| 0x930F | Signal vom Regenlichtsensor unplausibel |
| 0x9310 | Schliesszylinder defekt |
| 0x9311 | Lichtnotlauf mit Kl.15 aktiv |
| 0x9312 | Lichtnotlauf mit Geschwindigkeit aktiv |
| 0x9313 | Uebertemperatur FH-Fahrertuer |
| 0x9314 | Uebertemperatur FH-Beifahrertuer |
| 0x9315 | ALC-System defekt |
| 0x9316 | ALC-System: AL links abgeschaltet |
| 0x9317 | ALC-System: AL rechts abgeschaltet |
| 0x9318 | RLS Grund: Dunkelheit aber Abblendlicht aus |
| 0x9319 | FH-Fahrertuer denormiert |
| 0x931A | FH-Beifahrertuer denormiert |
| 0x931B | Analog-Schalter FH-Fahrertuer defekt |
| 0x931C | Analog-Schalter FH-Beifahrertuer defekt |
| 0x931D | Analog-Schalter Lenkstock Blinker links defekt |
| 0x931E | Analog-Schalter Lenkstock Blinker rechts defekt |
| 0x931F | Analog-Schalter Lenkstock Lichthupe/Fernlicht defekt |
| 0x9320 | LIN-Schalterblock FH-Fahrertuer defekt |
| 0x9321 | LIN-Schalterblock FH-Beifahrertuer defekt |
| 0x9322 | LIN-Schalterblock FH-Fahrertuer hinten defekt |
| 0x9323 | LIN-Schalterblock FH-Beifahrertuer hinten defekt |
| 0x9324 | LIN-Schalterblock zentraler FH-Schalter defekt |
| 0x9325 | LIN-Schalterblock Spiegelverstellung horizontal defekt |
| 0x9326 | LIN-Schalterblock Spiegelverstellung vertikal defekt |
| 0x9327 | LIN-Schalterblock Spiegelverstellung beiklappen defekt |
| 0x9328 | Taster Innenlicht defekt |
| 0x9329 | Taster Nebelscheinwerfer defekt |
| 0x932A | Taster Nebelschlusslicht defekt |
| 0x932B | Taster Warnblinklicht defekt |
| 0x932C | Schalter Rueckfahrscheinwerfer defekt |
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
| default | 0x01 | 0x02 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x02 | Sensorspannung | Volt | - | unsigned char | - | 5 | 255 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-lampnrtexte"></a>
### LAMPNRTEXTE

Dimensions: 33 rows × 3 columns

| LAMPNR | NAME | TEXT |
| --- | --- | --- |
| 0x00 | AUSGANG_FL_LINKS | Fernlicht links |
| 0x01 | AUSGANG_FL_RECHTS | Fernlicht rechts |
| 0x02 | AUSGANG_AL_LINKS | Abblendlicht links |
| 0x03 | AUSGANG_AL_RECHTS | Abblendlicht rechts |
| 0x04 | AUSGANG_BEGRL_LINKS | Begrenzungslicht links |
| 0x05 | AUSGANG_BEGRL_RECHTS | Begrenzungslicht rechts |
| 0x06 | AUSGANG_NSW_LINKS | Nebelscheinwerfer links |
| 0x07 | AUSGANG_NSW_RECHTS | Nebelscheinwerfer rechts |
| 0x08 | AUSGANG_FRA_LINKS_VORN | Fahrtrichtungsanzeiger links vorne |
| 0x09 | AUSGANG_FRA_RECHTS_VORN | Fahrtrichtungsanzeiger rechts vorne |
| 0x0A | AUSGANG_FRA_LINKS_HINTEN | Fahrtrichtungsanzeiger links hinten |
| 0x0B | AUSGANG_FRA_RECHTS_HINTEN | Fahrtrichtungsanzeiger rechts hinten |
| 0x0C | AUSGANG_E70_SML_LINKS_VORN_R56_CS_ORANGE | E70: Seitenmarkierungsleuchte links vorne, R56: Colour-Switch Orange |
| 0x0D | AUSGANG_E70_SML_RECHTS_VORN_R56_CS_BLAU | E70: Seitenmarkierungsleuchte rechts vorne, , R56: Colour-Switch Blau |
| 0x0E | AUSGANG_BREMSLICHT_LINKS | Bremslicht links |
| 0x0F | AUSGANG_BREMSLICHT_RECHTS | Bremslicht rechts |
| 0x10 | AUSGANG_BREMSLICHT_MITTE | Bremslicht mitte |
| 0x11 | AUSGANG_SL_BL_LINKS_1 | Schlusslicht/Bremslicht links 1 |
| 0x12 | AUSGANG_SL_BL_RECHTS_1 | Schlusslicht/Bremslicht rechts 1 |
| 0x13 | AUSGANG_E70_SL_BL_LINKS_2_R56_SML_LV_RH | E70: Schlusslicht links 2, R56: Seitenmarkierungsleuchte links vorne, rechts hinten |
| 0x14 | AUSGANG_E70_SL_BL_RECHTS_2_R56_SML_RV_LH | E70: Schlusslicht rechts 2, R56: Seitenmarkierungsleuchte rechts vorne, links hinten |
| 0x15 | AUSGANG_KZL | Kennzeichenlicht |
| 0x16 | AUSGANG_INNENBELEUCHTUNG | Innenbeleuchtung |
| 0x17 | AUSGANG_NSL_LINKS | Nebelschlusslicht links |
| 0x18 | AUSGANG_NSL_RECHTS | Nebelschlusslicht rechts |
| 0x19 | AUSGANG_RFL_LINKS | Rueckfahrlicht links |
| 0x1A | AUSGANG_RFL_RECHTS | Rueckfahrlicht rechts |
| 0x1B | AUSGANG_BFD_LINKS | Break-Force-Display links |
| 0x1C | AUSGANG_BFD_RECHTS | Break-Force-Display rechts |
| 0x1D | AUSGANG_DRL_LINKS | Tagfahrlicht links |
| 0x1E | AUSGANG_DRL_RECHTS | Tagfahrlicht rechts |
| 0x1F | AUSGANG_KLEMME_58G | Klemme 58g |
| 0xFF | UNKNOWN | unbekannte Lampe |

<a id="table-activetab"></a>
### ACTIVETAB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht aktiv |
| 0x01 | aktiv |
| 0xXY | signal ungueltig |

<a id="table-spiegel-heizung"></a>
### SPIEGEL_HEIZUNG

Dimensions: 9 rows × 3 columns

| WERT | TEXT | NAME |
| --- | --- | --- |
| 0x00 | Spiegelheizung aus | 0 |
| 0x01 | Spiegelheizung 25% ein | 25 |
| 0x02 | Spiegelheizung 50% ein | 50 |
| 0x03 | Spiegelheizung 75% ein | 75 |
| 0x04 | Spiegelheizung 100% ein | 100 |
| 0x05 | Spiegelheizung 125% ein | 125 |
| 0x06 | Spiegelheizung unbegrenzt ein | UNBEGRENZT |
| 0x07 | ungueltig | UNGUELTIG |
| 0xFF | falscher Eingabewert | ERROR |

<a id="table-spiegelheizungstat"></a>
### SPIEGELHEIZUNGSTAT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Spiegelheizung aus |
| 0x01 | Spiegelheizung 25% ein |
| 0x02 | Spiegelheizung 50% ein |
| 0x03 | Spiegelheizung 75% ein |
| 0x04 | Spiegelheizung 100% ein |
| 0x05 | Spiegelheizung 125% ein |
| 0x06 | Spiegelheizung unbegrenzt ein |
| 0x07 | ungueltig |
| 0xFF | falscher Eingabewert |

<a id="table-fh-richtung"></a>
### FH_RICHTUNG

Dimensions: 4 rows × 3 columns

| FH_R | NAME | TEXT |
| --- | --- | --- |
| 0x00 | NEUTRAL | Fenster nicht bewegen |
| 0x01 | OEFFNEN | Fenster oeffnen |
| 0x03 | SCHLIESSEN | Fenster schliessen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-auswahl-fenster"></a>
### AUSWAHL_FENSTER

Dimensions: 5 rows × 2 columns

| ARGUMENT | BESCHREIBUNG |
| --- | --- |
| 0x00 | Vorgang abbrechen |
| 0x11 | Fahrerseite |
| 0x12 | Beifahrerseite |
| 0x21 | Fahrerseite und Beifahrerseite |
| 0x40 | Alle |

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

<a id="table-auswahl-spiegel"></a>
### AUSWAHL_SPIEGEL

Dimensions: 3 rows × 3 columns

| SPIEGEL | NAME | TEXT |
| --- | --- | --- |
| 0x01 | SPIEGEL_FAT | Spiegel Fahrertuer auswaehlen |
| 0x02 | SPIEGEL_BFT | Spiegel Beifahrertuer auswaehlen |
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
| 0x05 | BEIKLAPPEN | Spiegel beiklappen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-steuern-digital-verfahren"></a>
### STEUERN_DIGITAL_VERFAHREN

Dimensions: 16 rows × 3 columns

| ARGUMENT | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | Vorgang Abbrechen | Vorgang Abbrechen |
| 0x11 | FH_FA_AUF | Fensterheber Fahrerseite oeffnen |
| 0x12 | FH_FA_ZU | Fensterheber Fahrerseite schliessen |
| 0x13 | FH_FA_MAUT_AUF | Fensterheber Fahrerseite Maut oeffnen |
| 0x14 | FH_FA_MAUT_ZU | Fensterheber Fahrerseite Maut schliessen |
| 0x15 | FH_BF_AUF | Fensterheber Beifahrerseite oeffnen |
| 0x16 | FH_BF_ZU | Fensterheber Beifahrerseite schliessen |
| 0x17 | FH_BF_MAUT_AUF | Fensterheber Beifahrerseite Maut oeffnen |
| 0x18 | FH_BF_MAUT_ZU | Fensterheber Beifahrerseite Maut schliessen |
| 0x19 | FH_FA_BF_AUF | Fensterheber Fahrerseite Beifahrerseite oeffnen |
| 0x1A | FH_FA_BF_ZU | Fensterheber Fahrerseite Beifahrerseite schliessen |
| 0x1B | FH_FA_BF_MAUT_AUF | Fensterheber Fahrerseite Beifahrerseite Maut oeffnen |
| 0x1C | FH_FA_BF_MAUT_ZU | Fensterheber Fahrerseite Beifahrerseite Maut schliessen |
| 0x30 | SPIEGEL_BEIGEKLAPPT | Spiegel einklappen oder ausklappen |
| 0x32 | SPIEGEL_HEIZUNG_EIN | Spiegelheizung |
| 0x70 | KISI_AKTIV | Kindersicherung aktiv |

<a id="table-tiefentl"></a>
### TIEFENTL

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 | 0x16 |

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

<a id="table-notl"></a>
### NOTL

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 |

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

<a id="table-bfdstufetexte"></a>
### BFDSTUFETEXTE

Dimensions: 9 rows × 3 columns

| BFD_STUFE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | KEINE_BFD | keine BFD-Stufe |
| 0x01 | BFD_0 | Bremslicht |
| 0x02 | BFD_1 | BFD-Stufe 1 |
| 0x04 | BFD_2 | BFD-Stufe 2 |
| 0x03 | BFD_0_1 | Bremslicht und BFD-Stufe 1 |
| 0x05 | BFD_0_2 | Bremslicht und BFD-Stufe 2 |
| 0x06 | BFD_1_2 | BFD-Stufe 1 und BFD-Stufe 2 |
| 0x07 | BFD_0_1_2 | Bremslicht und BFD-Stufe 1 und BFD-Stufe 2 |
| 0xff | ERROR | falsche Eingabe |

<a id="table-fh-einlernen"></a>
### FH_EINLERNEN

Dimensions: 7 rows × 2 columns

| CODE | BESCHREIBUNG |
| --- | --- |
| 0x00 | NO INIT STARTED |
| 0x01 | INIT RUNNING |
| 0x02 | INIT COMPLETED |
| 0x03 | ERROR BUSY |
| 0x04 | ERROR USER STOP |
| 0x05 | ERROR REVERSE |
| 0x06 | ERROR INIT |

<a id="table-stat-lenkstock-blinker"></a>
### STAT_LENKSTOCK_BLINKER

Dimensions: 13 rows × 3 columns

| WERT | VSWERT | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 0 | in Nullstellung |
| 0x01 | 0 | in Nullstellung |
| 0x18 | 1 | Blinker links dauer betaetigt |
| 0x08 | 2 | Blinker links tipp betaetigt |
| 0x09 | 2 | Blinker links tipp betaetigt |
| 0x06 | 3 | Blinker rechts dauer betaetigt |
| 0x02 | 4 | Blinker rechts tipp betaetigt |
| 0x03 | 4 | Blinker rechts tipp betaetigt |
| 0x20 | 5 | Fernlicht betaetigt |
| 0x21 | 5 | Fernlicht betaetigt |
| 0x40 | 6 | Lichthupe betaetigt |
| 0x41 | 6 | Lichthupe betaetigt |
| 0xFF | 7 | Mehrfachbetaetigung |

<a id="table-stat-lampen-defekte"></a>
### STAT_LAMPEN_DEFEKTE

Dimensions: 4 rows × 3 columns

| WERT | VSWERT | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 2 | Nicht Ueberwacht |
| 0x01 | 1 | Fehler |
| 0x02 | 0 | Ok |
| 0x03 | 1 | Fehler |

<a id="table-lampfunktexte"></a>
### LAMPFUNKTEXTE

Dimensions: 10 rows × 3 columns

| LAMPFUNK | NAME | TEXT |
| --- | --- | --- |
| 0x01 | AL | Abblendlicht |
| 0x02 | NSW | Nebelscheinwerfer |
| 0x03 | FL | Fernlicht |
| 0x04 | FRA | Fahrtrichtungsanzeiger |
| 0x05 | BL | Bremslicht |
| 0x06 | BFD_1 | BFD Stufe 1 |
| 0x07 | BFD_2 | BFD Stufe 2 |
| 0x08 | RFL | Rueckfahrlicht |
| 0x09 | TFL | Tagfahrlicht |
| 0x0A | NSL | Nebelschlusslicht |

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

<a id="table-eks-hersteller"></a>
### EKS_HERSTELLER

Dimensions: 4 rows × 2 columns

| NUMBER | TEXT |
| --- | --- |
| 0x00 | Kein Hersteller |
| 0x01 | BROSE |
| 0x02 | KUESTER |
| 0xFF | UNGÜLTIG |

<a id="table-kuester-ee-denorm-log"></a>
### KUESTER_EE_DENORM_LOG

Dimensions: 36 rows × 2 columns

| NUMMER | TEXT |
| --- | --- |
| 0x00 | Nichts |
| 0x01 | Beifahrertuer. ASCET-Schnittstelle fordert Denormierung |
| 0x02 | Beifahrertuer. Positionsfehler: Oberer Block zu frueh |
| 0x03 | Beifahrertuer. Positionsfehler: Oberer Block zu spaet |
| 0x04 | Beifahrertuer. Positionsfehler: Unterer Block zu frueh |
| 0x05 | Beifahrertuer. Positionsfehler: Unterer Block zu spaet |
| 0x06 | Beifahrertuer. Hallfehler: Hall A defekt |
| 0x07 | Beifahrertuer. Hallfehler: Hall B defekt |
| 0x08 | Beifahrertuer. Hallfehler: Hall Frequenz zu hoch |
| 0x09 | Beifahrertuer. Hallfehler: Hall Massefehler, zuwenig Pulse bis Block |
| 0x0A | Beifahrertuer. RAM-Fehler: Variable 'Position' korrumpiert |
| 0x0B | Beifahrertuer. RAM-Fehler: Variable 'Position OK' korrumpiert |
| 0x0C | Beifahrertuer. EEPROM-Fehler: Kodierdaten korrumpiert |
| 0x0D | Beifahrertuer. Relaisfehler |
| 0x0E | Beifahrertuer. Hallfehler: Zuviele Hallpulse ohne Motorbestromung |
| 0x0F | Beifahrertuer. EEPROM-Fehler: EEPROM-Positiondaten gehlerhaft |
| 0x10 | Beifahrertuer. Hallfehler: Hall-Richtung falsch |
| 0x11 | Beifahrertuer. EEPROM-Fehler: Nach Reset war Position nicht mehr gueltig |
| 0x81 | Fahrertuer. ASCET-Schnittstelle fordert Denormierung |
| 0x82 | Fahrertuer. Positionsfehler: Oberer Block zu frueh |
| 0x83 | Fahrertuer. Positionsfehler: Oberer Block zu spaet |
| 0x84 | Fahrertuer. Positionsfehler: Unterer Block zu frueh |
| 0x85 | Fahrertuer. Positionsfehler: Unterer Block zu spaet |
| 0x86 | Fahrertuer. Hallfehler: Hall A defekt |
| 0x87 | Fahrertuer. Hallfehler: Hall B defekt |
| 0x88 | Fahrertuer. Hallfehler: Hall Frequenz zu hoch |
| 0x89 | Fahrertuer. Hallfehler: Hall Massefehler, zuwenig Pulse bis Block |
| 0x8A | Fahrertuer. RAM-Fehler: Variable 'Position' korrumpiert |
| 0x8B | Fahrertuer. RAM-Fehler: Variable 'Position OK' korrumpiert |
| 0x8C | Fahrertuer. EEPROM-Fehler: Kodierdaten korrumpiert |
| 0x8D | Fahrertuer. Relaisfehler |
| 0x8E | Fahrertuer. Hallfehler: Zuviele Hallpulse ohne Motorbestromung |
| 0x8F | Fahrertuer. EEPROM-Fehler: EEPROM-Positiondaten gehlerhaft |
| 0x90 | Fahrertuer. Hallfehler: Hall-Richtung falsch |
| 0x91 | Fahrertuer. EEPROM-Fehler: Nach Reset war Position nicht mehr gueltig |
| 0xFF | Ungueltig |

<a id="table-lednrtexte"></a>
### LEDNRTEXTE

Dimensions: 4 rows × 3 columns

| LEDNR | NAME | TEXT |
| --- | --- | --- |
| 0x00 | AUSGANG_FLC_LED | Automatische Fahrlicht Kontrolle LED |
| 0x01 | AUSGANG_WHF_LED | Warnblinktaster Beleuchtung LED |
| 0x02 | AUSGANG_ILUM_PFIE_LED | Vorfeldbeleuchtung LED |
| 0xFF | UNKNOWN | unbekannte LED |
